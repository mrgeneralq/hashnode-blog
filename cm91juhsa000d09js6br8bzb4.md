---
title: "Understanding Client-to-Server Delegation in ServiceNow"
seoTitle: "Client-to-Server Delegation in ServiceNow"
seoDescription: "Client-to-server delegation in ServiceNow enhances security, performance, and scalability by centralizing logic and ensuring efficient processing"
datePublished: 2025-04-03T16:07:32.746Z
cuid: cm91juhsa000d09js6br8bzb4
slug: understanding-client-to-server-delegation-in-servicenow
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1743618311157/0e3c5c97-6940-4d0e-8060-6311513c6fa0.jpeg
tags: client, servicenow, client-server-architecture

---

> In this chapter we will be looking into the different scenario’s for delegating client side responsibilities to the server. We will explain why this is essential, and how this automatically becomes a more scalable solution.

# What is client-to-server delegation?

Client-to-server delegation is the practice of moving responsibilities executed from the client-side to the server-side. Client-to-server delegation also involves the art of identifying when certain logic has to be processed by the server instead of the client. This relates not only to scripting but also to the practice of identifying the right artifact(s) for a specific use case.

# Why Use Client-to-Server Delegation?

## Enhanced Security **🔒**

When designing your solution, you should be very aware that everything executed on the client side **can be manipulated**. Everything processed on the server side is out of reach for the user to manipulate. This is also why UI policies or other client-side artifacts should never be considered for implementing security. If the goal is to secure something, you should always rely on the **ACLs**.

## Centralized business logic **🧩**

Keeping all your business logic on the server allows for easier (and real-time) updates. We also ensure that all the logic is centralized in one place. Having all business logic centralized in one place is not only good for consistency but also ensures we can easily modify the business logic afterward, without the need to modify the client.

## Improved client performance **🚀**

The more calculations handled by the server, the better the end-user’s experience becomes. Transferring more logic to the server-side results in quicker processing on the client side, thus resulting in an overall better user experience.

## Scalability **📈**

Because all the business logic is consolidated on the server side, we can easily scale our solution without the need to change all the logic on the client side. Think of it this way: the server offers plenty of possibilities for reusability, while the client is not designed for this.

# When to delegate to the server?

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text"><em>There are few rules that could decide when something functionality has to be delegated to the server. Here are a few examples with their explanation:</em></div>
</div>

### **Data validations** ✅

When data is validated, we often have a validation in place on the client side. For example, checking if a user with a given email address already exists before creating a new user. Although it’s highly recommended to provide this feedback on the client side, it’s crucial to ensure this validation also takes place on the server side.

### **Complex calculations** 🧮

The heavier the calculations, the more the client might experience some performance issues. Delegating the complex calculations to the server unloads the client from heavy calculations and essential processing power.

### **Business logic** 🏢

If the logic you are trying to implement is directly connected to business logic, it should always be delegated to the server. This ensures the centralization of all business logic on the server-side.

### **Security related** 🔐

In case it’s security-related, such as access validations, this should always take place on the server side. If not processed server-side, it’s unsafe and can be bypassed.

### Date Time calculations/validations ⏰

Date Time validations are very often executed on the client, but this is actually not a reliable approach because date and time calculations can become very complex. For example, timezones and schedules are all unknown to the client.

### Different types of clients 📱💻

Client implementations can be very dependent based on the device. Implementing the logic on the client-side would potentially require multiple implementations for multiple devices for the same client. By limiting the client responsibilities to the bare minimum and delegating it to the server would make it easier to onboard new client types. Think of Mobile, portal, workspaces, …

## Example decisions for client-to-server delegation 📊

It can still be challenging to understand when something has to be delegated, as use cases can become very specific. If you consider the earlier mentioned criteria as a rule of thumb, you will most likely cover the majority of situations. Because client-to-server delegation could also mean something is being executed/validated on both client and server, I will provide you with some practical examples below.

---

* **Email Validation**:
    
    * **Client**: ✅
        
    * **Server**: ✅
        

**Explanation**: Email validation should be strict and initially validated on the client side to provide immediate feedback to the user. However, it is crucial to also validate on the server side to ensure data integrity and security.

---

* **Date Time Calculations**:
    
    * **Client**: ❌
        
    * **Server**: ✅
        

**Explanation**: Date and time calculations should be processed on the server to ensure consistent validation across all date and time fields, taking into account time zones and other complexities.

---

* **Subcategory Visibility**:
    
    * **Client**: ✅
        
    * **Server**: ❌
        
    * **Explanation**: Making the subcategory field visible when the category is selected can be handled on the client side. Since it has no business impact, securing it with ACL is unnecessary.
        

---

* **Fields Read-Only Post-Closure**:
    
    * **Client**: ❌
        
    * **Server**: ✅
        
    * **Explanation**: Making all fields read-only after the ticket is closed should be enforced on the server side. This prevents any updates that could trigger notifications or cause unexpected behavior, ensuring data consistency and security.
        

---

## Bonus example: Single catalog item 📦

Another great example is a use case where we reuse catalog items for multiple personas. I often see catalog items containing logic to check if the user has a given role; if so, the user is presented with additional fields for that persona.

Calculating field/variable visibility based on roles is possible but is not considered a secure implementation. Instead, consider using the "roles" field on the variable.

Is the calculation more complicated and does it not only depend on having a role? In such cases, you should always consider creating a separate catalog item for a different audience. You would protect this on the server side using the User Criteria.

# Conclusion 🏁

Identifying situations for client-to-server delegation is essential to ensure not only the security of your application but also to enhance the overall user experience by unloading the client from heavy processing. You are also prepared for possible changes to the business logic without the need to modify the client behavior. We also ensure the readiness for onboarding of new client by limiting the client responsibilities to the bare minimum.

When identifying this, we should carefully evaluate whether the task responsibility should be executed on the client, the server, or both. This, however, would be very dependent on the use case.

We learned that we should try to limit the client side functionality to the bare minimum on what is essential for the client. We learned how to determine when something is supposed to run on the client and when on the server side.