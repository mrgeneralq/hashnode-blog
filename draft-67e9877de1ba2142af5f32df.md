---
title: "Deepdive example delegation"
slug: deepdive-example-delegation

---

Common violations of client to server delegation

## Example use case **📚**

We got the following (catalog) onChange client script checking for changes on a reference field “Department”. Depending on the selected company, we want to only show a list of available categories relevant for that department.

## How NOT do it **❌**

Let’s first have a look on how it should not be done, empathizing the need of delegating to the server.  
The following example has multiple if statements, checking the sys\_id value. If the value matches the ID of the given department.

```javascript
function oChange(){

var department = g_form.getValue('department');

// IT Department
if(department == '3bnmc0x5zptagsgljsdrq3ib8wz4cg08'){
//populate choices
}

// HR Department
if(department == 'x38r5yylldql7xkxfmsjbe5qaak294cf'){
//populate choices
}
}
```

There are numerous reasons why this can be considered the wrong approach.

❌ Violation of the Open Closed principle  
❌ Everything on the client runs from your browser and can be manipulated  
❌ This violates the best practices by using hardcoded sys\_id’s

## Delegating to the server

The first challenge is to identify what is the logic that remains on the server, and what is on the client. A good rule of thumb, all the business logic should be delegated to the server. How the client-side utilizes the results depends on the use case.

Looking at our example, the business logic is to fetch a list of available Categories for a given department.  
This means, the only parameter that is required to fetch these results is the “Department” value.

So instead of running all our logic on the client, we move it to the server side. This is what our script include would look like:

```javascript
var DepartmentService = Class.create();
DepartmentService.prototype = {
    initialize: function() {},


    getCategoriesFromDepartment: function(department) {

		var results = [];

        // IT Department
        if (department == gs.getProperty('prefix.department.it')) {
            results.push(
				{value: 'it_services', displayValue:'IT Services'},
				{value: 'network', displayValue: 'Networking'}
			);
        };

        // HR Department
        if (department == gs.getProperty('prefix.department.hr')) {
            results.push(
				{value: 'onboarding', displayValue:'Employee onboarding'},
				{value: 'offboarding', displayValue: 'Employee offboarding'}
			);
        }

		return results;

    },

    type: 'DepartmentService'
};
```

Let’s break down the changes that took place:

We prepare a script include