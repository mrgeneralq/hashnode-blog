---
title: "To Scope or not to Scope"
seoTitle: "Scoping: Deciding When It's Necessary"
seoDescription: "Learn benefits and considerations of scoped applications in ServiceNow, and when to choose them for your solutions"
datePublished: 2025-08-25T04:00:34.794Z
cuid: cmeqla9yi000602jo32exbvtc
slug: to-scope-or-not-to-scope
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1755986311108/3f7bbe05-04c5-4733-ae8a-d62a016cff76.png
tags: application-development, servicenow

---

Scoped application development has increasingly become a default and best practice for implementing solutions on the ServiceNow platform. But should every custom implementation be part of a scope? Is building a scoped app always the right approach? Which artifacts should be part of the scoped application, and how do I ensure no other development is obstructed? In this article, I will provide you with my vision and reasoning on scoped application development, when to use them, and why it’s not always the right approach.

---

# Why scoped applications?

Let’s face it, there are numerous reasons to use scoped applications, and rightfully so. In today's rapidly evolving technological landscape, organizations are constantly seeking ways to enhance their operational efficiency.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1755587604095/52949a5d-279d-42d2-8f29-2c895e5e5860.png align="left")

## Isolation of the artifacts

When using scoped applications, all artifacts created as part of the application are by default protected and isolated from the remaining artifacts on the platform. This allows organizations to add new business logic onto the platform without needing to customize existing artifacts.

## Centralization of the business logic

A scoped application is built to serve a specific purpose for the organization. Whether it’s an integration with a 3rd party application or an advanced ticket assignment solution, each application is built to serve a specific purpose.

## Version control & collaboration

One of the most powerful advantages of using scoped applications is version control. Version control provides a centralized approach to effectively manage versions of your application. With this version control also comes the collaboration aspect, which allows multiple developers to work on different artifacts at the same time.

---

# Evaluating the need for a Scoped Application

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1755590858147/80a8b936-f656-4bf8-94fc-d58f95c3ea3c.png align="center")

Before you decide to create a scoped application, you should ask yourself some questions. By getting answers to those questions, you will better understand if going for a scoped application is the right approach.

1. ## Non existent in the ServiceNow
    

Your business or customer requires a solution that isn’t covered by any existing ServiceNow products. ServiceNow is a large platform with a wide variety of products, but use cases can vary, as can application needs. If it doesn't exist, you can create a custom application in ServiceNow to meet the requirement.

2. ## Expanding an existing product
    

You are using an existing ServiceNow product or an application from a completely different vendor, but some additional business logic is required for your business to use the application. This is another great example of when to use a new scoped application. *(more on that later in this article …)*

3. ## Building a spoke
    

ServiceNow does it, and so should you. If you need to build a new integration, you will benefit from having it defined under a separate scope. This approach ensures that the integration is isolated, making it easier to manage, update, and maintain without affecting other parts of the system.

---

# Defining the purpose

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1755985592789/c072cb05-b752-425c-bb37-ce8e3eaa70da.png align="center")

There is no use in building an application without being aware of its purpose. Building an application makes sense if its purpose is well defined. Some questions you should ask:

* What is the primary purpose of my application, and how is it going to help our business?
    
* Does it benefit from being self-contained?
    
* How does the application align with the organization's strategic goals?
    

*Defining the purpose of your application serves as the foundation for determining whether scoping the application is the right choice or if it would merely lead to unnecessary overhead.*

---

# Determining the Application Scope

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1755592010506/5b2987bf-ba38-4d90-adab-1347b8835f60.png align="center")

We now have a better understanding of when to build a scoped application. How do we decide which artifacts should be part of our application? It's quite easy to exceed the initially defined purpose of your application by incorporating the implementation of your use cases into the application scope. To simplify making the right choice, you can use my following thought process to define whether the artifact should be included or excluded within the application scope.

> Anything that is absolutely necessary to define **WHAT** the application does should be part of the application scope. Anything that describes HOW the application behaves should be considered configuration for the application and not be part of the scope.

This process helps in making clearer decisions about which artifacts are essential to the application's core purpose and when something should be configurable, but not necessarily part of the same scope.

---

# Choosing the Right Scope

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1755983338543/76947d3f-dc6d-454e-863c-757fae67f593.png align="center")

When working with existing applications or configuring your own application, you may question which application scope you should use for the configuration.

*Each application is responsible on its own to foresee it's necessary artifacts to fulfill the business requirements. An application may have a dependency on another application but only if the parent application has been foreseen and allows other applications to further extend how the application behaves. Should be part of a scope.*

*If the artifacts you are adding are not part of a broader use case, or are likely to be changed again over time, you should not create an application just to put the artifact in a scope. Instead, create them under the* ***global scope***.

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text"><em>Creating artifacts in the global scope is completely fine if there is no clear purpose for an application. Even if the artifacts are not in scope, with a well maintained deviation management process and high quality documentation standards, you can still maintain such configuration and avoid configuration drift.</em></div>
</div>

Creating the artifacts as part of the same application scope essentially changes the defined purpose and is thus not the right choice. An application is built to serve a specific purpose and has a pre-defined function.

## **Expanding the application purpose**

In case you need to expand the business logic, consider building an application that has a dependency on the base application instead. If the logic you are trying to add is not a good candidate for an application, create it under the global scope and document it properly.

## **Modifying the application purpose**

In case you have to change the existing behavior of the application that cannot be achieved by its provided configuration, you will have no other choice than modifying the artifact as part of the same application scope. It’s equally important to properly document this deviation to ensure the maintainability of the platform.

---

<div data-node-type="callout">
<div data-node-type="callout-emoji">📰</div>
<div data-node-type="callout-text"><strong>BONUS</strong>: I created a quick cheat sheet which you can find <a target="_self" rel="noopener noreferrer nofollow" href="https://blog.quintenvdb.net/scoped-app-cheat-sheet" style="pointer-events: none">here</a></div>
</div>

# Conclusion

> Scoped application development on the ServiceNow platform provides isolated, centralized, and well-managed solutions. However, not every custom solution needs to be scoped. Before creating a scoped application, check if there is a specific need, like missing features in ServiceNow or the need to expand an existing product. Make sure it serves a clear purpose and matches strategic goals. Decide which parts should be included based on the application's main functions. Use the global scope when specific scoping isn't necessary.