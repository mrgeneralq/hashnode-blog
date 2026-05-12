---
title: "Why Flow Designer Isn't My First Choice"
seoTitle: "Flow Designer: Why It's Not My Top Pick"
seoDescription: "Explore the benefits and challenges of using Flow Designer in ServiceNow, and understand why it may not be the best tool for all automation scenarios"
datePublished: 2025-03-30T10:20:37.808Z
cuid: cm8vhoy7k000908lead9q6gih
slug: why-flow-designer-isnt-my-first-choice
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1743326386696/15bc3e11-f41e-4ec0-8b4e-0e47a47c19c6.jpeg
tags: flow, servicenow, flow-designer

---

I am often associated with someone who "hates" flow designer. To be quite honest, no, I don’t hate flow designer. I do believe that flow designer was a great addition to the ServiceNow platform, if not the best in the past few years.

So, what is it that bothers me about flow designer? To understand that, let's first dive into why flow designer really made a difference.

## The flow designer made a difference due to its intuitive design.

Flow designer offers a very intuitive design, allowing even the most non-technical people to build simple flows. The drag-and-drop mechanics and the visual aspects in flow make the process of setting up flows very quick.

The drag-and-drop pill mechanics are easy to understand and make the process of automating your workflow like a walk in the park. The return types are neatly displayed next to the data pills, making it very clear which data pills should be used.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1743318796693/8852be56-aa70-40e7-9858-aa2f17aaa048.png align="left")

## Building Integrations with ease

One of the main benefits of Flow Designer is, without a doubt, the “[spokes](https://www.servicenow.com/docs/bundle/yokohama-integrate-applications/page/administer/integrationhub/reference/spokes-list.html).” Spokes are essentially the building blocks for integrating your workflow with third-party systems. Building integrations from scratch is very time-consuming and can only be done with extensive technical knowledge about both ServiceNow and the third-party application you are trying to integrate with. Thanks to the spokes, it’s just a matter of dragging and dropping the blocks in your flow and using the results to integrate them with your workflows.

## The executions tab

Another great addition to Flow designer is the “executions” tab. This view literally represents a history of all your executions and allows you to easily monitor the data flows, making it an essential tool to troubleshoot misconfigured flows.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1743321697931/d674d248-c6f7-467d-8047-4e97ba20c33a.png align="center")

# What I don’t like about flow designer

As mentioned earlier, all the things above have made a difference in how quickly we automate workflows, which is great. But ServiceNow has created a vision where every form of automation is always done through Flow Designer.

I remember an old video when Flow Designer was introduced by the well-known Chuck Tomassi, where he mentioned, “Script gurus, this is for you … stop writing code and use Flow Designer.”

Yes, Flow Designer is a great tool, and it does make automation extremely simple. But I don’t see Flow Designer as a replacement for everything. Back in the days when Flow Designer didn’t exist yet, we knew exactly where to look if something went wrong.

## Reverse engineering became a pain

As a reverse engineering enthusiast, I gave multiple sessions on how to properly reverse engineer by applying a logical way of thinking and reverse-thinking the process.

Let me clarify that sentence using an example:

*When submitting a new incident, the company field is automatically populated after the record is created.*

So the logical thinking process would be: It runs on the Incident table, it happens after the record is created, and it automatically populates the company field.

Breaking it down:

| **What is happening?** | Company field is updated |
| --- | --- |
| **Where is it happening?** | On incident table, server |
| **When is it happening?** | Company field is updated |

So, applying the logical thinking process, we know where to look:  
A business rule on the Incident table (insert true), with a script or action to update the company field (script contains company).

This simple technique was, in many cases, an effective approach to troubleshoot and reverse engineer errors. Now that flow designer has been introduced, this can also be hidden in a flow.

UI actions execute a piece of code when clicked on, except they can now also trigger a flow.

## Single responsibility

Just as covered in the series “[SOLID Principles](https://blog.quintenvdb.net/series/servicenow-solid)”, I do believe that applying the Single Responsibility principle does not only apply to code but also to the platform.

Business rules execute logic during CRUD operations of a record, UI actions execute code when interacting with clickable UI components, Assignment rules control the assignment, etc.

Having different artifacts, all serving their own purpose, is what keeps the platform maintainable. Having everything crammed into a single solution that covers all quickly shows its caveats.

### We have the executions tab, right?

Yes, definitely. However, finding the correct execution is what makes it challenging. Currently, the flow designer doesn't allow filtering by things like table, conditions, or actions, which makes it very difficult to locate specific tasks.

## So what does flow designer mean to me?

Flow designer serves a great purpose for automating a set of activities as part of a process, such as integrations. If you have a list of activities that need to occur in sequential order, a flow is what I would use.

But if the goal is to update a field after a record is updated, that is not a flow for me, but a business rule.

# Conclusion

Although the flow designer is a great tool for automation, it's important to understand its limitations and the drawbacks of overusing it. If you decide to use it (and you should), ensure you have proper governance around the creation and maintenance of your flows.

<div data-node-type="callout">
<div data-node-type="callout-emoji">📣</div>
<div data-node-type="callout-text">Make sure to <strong>subscribe </strong>to the newsletter if you want to know when the article releases on how to properly govern your flows</div>
</div>