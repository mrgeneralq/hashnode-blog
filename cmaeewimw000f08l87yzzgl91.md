---
title: "Everything You Need to Know About Events in ServiceNow"
seoTitle: "Everything You Need to Know About Events in ServiceNow"
seoDescription: "Learn to create, name, and use events in ServiceNow. Discover best practices for event abstraction and business logic expansion"
datePublished: 2025-05-07T20:49:51.704Z
cuid: cmaeewimw000f08l87yzzgl91
slug: everything-you-need-to-know-about-events-in-servicenow
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1746649599045/83670050-1d2b-4614-8312-3573b7169a89.png
tags: architecture, events, servicenow

---

> In ServiceNow, you can create something called an "event." These events are a powerful feature that can trigger numerous results as part of something happening in the platform. Yet, even the most experienced developers seem to misunderstand what an event is actually used for, how to name them, and furthermore, when and how to use them.

## What is an event? 📅

An event represents **something happening**. In ServiceNow, this is no exception. An **event** in ServiceNow **represents something happening on the ServiceNow platform**. Some examples of events in ServiceNow are:

* attachment.read
    
* task.approved
    
* login
    
* mid\_server.down
    

<div data-node-type="callout">
<div data-node-type="callout-emoji">ℹ</div>
<div data-node-type="callout-text">An overview of all events can be found in the the “<strong>sysevent_register</strong>” table.</div>
</div>

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1746648087784/827e6b8f-4e82-4810-a94e-0088e99a2f82.jpeg align="left")

Events are pushed into the event queue, after which they will be processed by the listeners.

## An event describes What Is Happening, Not What Should Happen 🔄

A mistake I often see is events being written with the purpose of making something happen. Let’s look at a specific example:  
*incident.send\_reminder\_email*

This example event describes what should happen, making this event only applicable for sending out a reminder email. This is **wrong** and not how events are supposed to be used.

Instead of sending out the event to trigger an email reminder, define an event that could result in sending out a reminder email. For example:

*incident.pending\_approval.wait\_time\_exceeded*

In this case, we can define one or more triggers that should each act in their own way based on the occurrence in the system. Some example triggers are:

* Execute a flow
    
* Send out a notification
    
* Run a script action
    

Each trigger has its own purpose and reason to act based on the event.

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">An event should always describe what happend, not what should happen.</div>
</div>

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1746647286110/828d0184-d02f-4bc9-9224-38b08c8440f4.jpeg align="left")

## Understanding abstraction for events 🧩

ServiceNow is not an OOP (Object-Oriented Programming) based platform. Therefore, extending events in ServiceNow is not an option. However, you can still make use of abstraction in events because of how business rules work in ServiceNow.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1746646852481/fe61d395-5541-4aa9-a78b-715022fc27ff.jpeg align="left")

Let’s take the following examples:

| **event** | **description** | **implementation** |
| --- | --- | --- |
| task.updated | triggers when a task record is updated | business rule on task table |
| incident.updated | triggers when an incident got updated | business rule on incident table |

If you implement the event calling based on the table described above, updating an incident record would trigger both the incident.updated and the task.updated events. This is **because** the **incident table extends** the **task table**, and thus the business rules of the task apply to the incident table.

This is where the power of abstraction comes into play. We could define a trigger on the incident.updated to act only upon incident updates, while at the same time, we might want something completely different to happen that should apply to all task records. Something that wouldn’t be directly tied to any process, but more to the platform itself.

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">You should focus on listening for the specific events you need rather than the abstract ones.</div>
</div>

## Expand business logic without customization 😊

Events are also very effective for listening to changes in other applications. When creating your application, consider defining events for certain occurrences in your application, even if you don’t have an immediate implementation for them yourself. This would allow other applications or implementations to listen for these events and act upon them. This is one of the many ways to allow others to build functionality on top of your application without needing to change anything in the application.

## Conclusion 🏁

> In ServiceNow, events are very important because they mark when something has happened. Events are meant to describe occurrences, not dictate what should be done next. Issues can arise if one attempts to do too much. A frequent example of this would be naming events after the actions they cause instead of the situation that brought them into that scenario. For instance, better defining an event does wonders for clarity. It’s better to describe “incident.pending\_approval.wait\_time\_exceeded” because it is much more informative. Describing it as “incident.send\_reminder\_email” shifts the focus to response, not the trigger, which defeats the purpose.
> 
> It can be beneficial to think about abstraction when designing events, even if an object-oriented framework is not the base of ServiceNow. This is especially useful because business rules tend to cascade through related tables. That leads to more specific event listeners rather than wide-net listeners. That is when the power of the platform really stands out.