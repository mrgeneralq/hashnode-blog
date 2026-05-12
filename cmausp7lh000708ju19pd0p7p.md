---
title: "What Is Conditional Table Query Range ACL?"
seoTitle: "Understanding Conditional Table Query Range ACL"
seoDescription: "ServiceNow introduces a new ACL type, conditional_table_query_range, for table-level operations and security checks using GlideSecurityManager"
datePublished: 2025-05-19T08:00:24.245Z
cuid: cmausp7lh000708ju19pd0p7p
slug: what-is-conditional-table-query-range-acl
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1747641561957/01f1b93f-5532-4e85-8e34-60aa878c52cf.png

---

*Earlier this month, ServiceNow rolled out a security change involving new ACL types for which they are mostly documented. Yes, mostly 👀 . We know about query\_range and query\_match, but have you seen this* ***conditional\_table\_query\_range***?

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1747640723798/27530708-08b7-4fa8-8725-fb997b336ed4.png align="center")

## How does it work?

These ACL are different from the regular ACL's. They are defined on table level. As you might have noticed, some of the ACL contains a security attribute starting with SAB\_. In these attributes you will find a line of code that looks like this:

```javascript
new global.SNCAPICallWrapper().hasRightsToConditionalTableQueryRange(['SOME_TABLE_NAME'])
```

At first you might think, this is blackbox, trying to open the reference gives a record not found. In reality, ServiceNow is **just hiding** this **script include** using a before query business rule on the script include table. You can find the link to the business rule here.

<div data-node-type="callout">
<div data-node-type="callout-emoji">🔗</div>
<div data-node-type="callout-text"><a target="_self" rel="noopener noreferrer nofollow" href="https://YOUR_INSTANCE.service-now.com/nav_to.do?uri=sys_script.do?sys_id=349c387f3bf422102d14299a04e45ab8" style="pointer-events: none">HideSNCAPICallWrapper</a></div>
</div>

After you disabled the business rule, you will have access to the hidden script include.

<div data-node-type="callout">
<div data-node-type="callout-emoji">🔗</div>
<div data-node-type="callout-text"><a target="_self" rel="noopener noreferrer nofollow" href="https://YOUR_INSTANCE.service-now.com/nav_to.do?uri=sys_script_include.do?sys_id=c49990f73bf022102d14299a04e45a62" style="pointer-events: none">SNCAPICallWrapper</a></div>
</div>

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1747637660262/9f2b8281-bfcf-4b1f-abda-ac952ba8ef0a.png align="center")

In that script include, we can find the function that is called by our security attribute.

```javascript
	// work-around for making GlideSecurityManager.get() call available from scoped apps
	hasRightsToConditionalTableQueryRange: function(tableName) {
		var path = 'record/' + tableName + '/conditional_table_query_range';
		var gsm = global.GlideSecurityManager.get();
		return gsm.hasRightsTo(path, new GlideRecord(tableName));
	},
```

This piece of code is calling the [GlideSecurityManager](https://www.servicenow.com/docs/bundle/yokohama-api-reference/page/app-store/dev_portal/API_reference/GlideSecurityManager/concept/GlideSecurityManagerAPI.html) and evaluates based on the ACL operation and the given table name, if access is granted or not. So if we link all of this logic together, we get the following logical chain:

ServiceNow has multiple query range ACL, some query range ACL contain a security attribute. The security attribute decides if the ACL will evaluate to true or false. The security attribute contains the line of code making a call to our SNCAPICallWrapper script include with it’s corresponding table name.

The wrapper itself contains a hardcoded line to evaluate the result of the ACL, which will assess record access for the provided table name for all ACLs with the operation "**conditional\_table\_query\_range**." If the ACL evaluates to true, the attribute will also return true, and the ACL will grant access.

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">The <strong>conditional_table_query_range </strong>ACL is considered a boilerplate ACL containing a set of foundational checks required to pass for a table. The ACL do not evaluate automatically and need to be called via the GlideSecurityManager using the Security Attributes.</div>
</div>

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1747639988290/38c7cf60-3ce4-4b6c-abba-4cdbfe7cd7ac.jpeg align="center")

## What is the use case for this ACL?

These ACL’s have been generated automatically and are considered a boilerplate ACL which may contain a set of security checks that always need to evaluate to true in order to gain access. You can have multiple table.\* or even table.field ACL’s call the boilerplate ACL to evaluate the access.

## Conclusion

> ServiceNow recently introduced new ACL types, including conditional\_table\_query\_range, which operate at the table level and involve hidden script includes like SNCAPICallWrapper. These ACLs use the GlideSecurityManager to determine access rights based on specific security attributes. They serve as boilerplate ACLs, requiring certain checks to evaluate true for access, influencing multiple table-level or field-level ACL evaluations.