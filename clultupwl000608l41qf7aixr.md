---
title: "Single responsibility: Script includes"
seoTitle: "Script embodies single responsibility principle"
seoDescription: "Enhance ServiceNow development: use single responsibility script includes for better maintenance, fewer bugs, and fewer development conflicts"
datePublished: 2024-04-04T22:47:27.909Z
cuid: clultupwl000608l41qf7aixr
slug: single-responsibility-script-includes
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1712697194582/572350c0-bc13-4b35-bf5e-126b8798c994.png
tags: javascript, developer, servicenow, servicenow-cad

---

When I set up my script includes for an application, I carefully think about the single responsibility to get optimal application design. Single responsibility is one of the five principles of **S**OLID.

Note however that applying all the SOLID principles is not quite possible within the ServiceNow platform.

## Single Responsibility

Giving every script include it's own specific responsibility will drastically improve your development experience within the platform. At a certain point you will realize that some code becomes very repetitive but is not generic enough to be migrated to another private function.

In this case, consider moving the logic towards another script include.

Take the following example:

| Name | Responsibility |
| --- | --- |
| OnboardingService | This script include contains all business logic for the onboarding process. |
| OnboardingServiceREST | This script include is processing and interacting with another HR onboarding application using REST. |

Because we **contained** all **REST** specific **logic within** it's **own script include**, we reduced the risk of breaking anything that is not REST related.

**Whenever you identify a functionality that does not belong within the script include, consider creating a new script include for it's purpose.**

<mark>This doesn't mean you have to create script includes for every individual functionality.</mark> Carefully think about the end goal you are trying to achieve. It's very easy to over engineer this and create script includes for every single thing.

## More scripts **≠** Over engineering

I often hear from others that I am creating script includes for no particular reason. I do in fact consider creating many scripts, but I use the following rule to decide if it's worth creating a new script include:

<mark>If the logic has a purpose that doesn't belong anywhere else </mark> **<mark>AND </mark>** <mark>that purpose is high likely to be expanded afterwards with similar functions, it means it can be transfered to another script include.</mark>

Some more examples I personally apply:

| Script include | Purpose |
| --- | --- |
| IncidentService | This script include contains all business logic for the process. Whenever anything changes in the business logic, we know we should be able to find this here. |
| IncidentServiceRefQual | Script include containing all functions only being called by reference qualifiers. We separate this from the normal IncidentService because these functions will all expect the same input (being the current record), but also because they all have one thing in common, **they all return an encoded query** (which is needed for the reference qualifier). |
| IncidentServiceSchedule | Containing all functions that will be called from a scheduled jobs. Although this sounds useless, <mark>Scheduled jobs are NOT captured in update sets and changes are NOT </mark> **<mark>tracked</mark>**. If we would accidently update our scheduled job we would have no way to revert the changes. To overcome this issue, we contain all scripts being called from a scheduled job in it's own Script include. If we ever accidently update our scheduled job, all we need to manually type is 1 line of code, all the actual logic is contained safely in our Schedule layer. |

## Why you should apply this principle

**Maintainability**  
Separating logic across different script includes ensures that everything remains very maintainable. Whenever a particular part of the application has to be expanded or changed, you know exactly which script include to open.

**Prevent bugs**  
Each script having it's own responsibility will reduce the chance of introducing bugs potentially breaking your application.

**Reduce conflicting development**  
If all code would be present in one script include only, the chance that you will come across a moment where you and someone else require to work on the same script will drastically increase.

## There is no right or wrong

Every customer, environment and ideally developer will have it's own way of setting up the scripts. What matters most is that in the end, not only you, but also others should be able to read and maintain your code, and understand what is going on.

I personally use these principles as the foundation of a more expanded thought process, for which I still today on a frequent base see extra use cases popping up, fitting the puzzle pieces together.