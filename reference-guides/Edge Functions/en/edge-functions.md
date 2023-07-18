---
title: Edge Functions
description: Azion Edge Functions allow you to create event-driven, serverless applications, at the edge of the network, closer to users.
meta_tags: edge functions, edge computing
namespace: documentation_products_edge_functions
permalink: /documentation/products/edge-application/edge-functions/
---

Azion **Edge Functions** allows you to create event-driven, serverless applications, at the edge of the network, closer to users.

With Edge Functions, you can perform serverless functions in response to events on edge nodes of our network with no need of having or managing servers.

Explore how to use and get the most out of Edge Functions as follows.

---

## About Edge Functions

Here are some of the solutions provided by Azion **Edge Functions**.

You can use functions to handle HTTP in the following Request and Response phases:

- As soon as a user's requests are received in the *Edge Node* (Viewer Request).
- Before the Azion *Edge Node* forwards the Request to the Origin (Origin Request).
- As soon as the *Edge Node* gets the response from the Origin (Origin Response).
- Before the Azion *Edge Node* forwards the response to the user (Viewer Response).

You can also generate responses without necessarily having to forward the request to the origin.

By using Edge Functions on your **Edge Application**, you can create a variety of solutions, for example:

- Inspect cookies to rewrite URLs to different versions of a site for A/B testing.
- Send different objects to your users based on the User-Agent header, which contains information about the device that submitted the request. For example, you can send images in different resolutions to users based on their devices.
- Inspect headers or authorized tokens, inserting a corresponding header and allowing access control before forwarding a request to the origin.
- Add, delete, and modify headers and rewrite the URL path to direct users to different cache objects.
- Generate new HTTP responses to do things like redirect unauthenticated users to login pages or create and deliver static webpages right from the edge.

See more ways of using Edge Functions [in Guides](/en/documentation/products/guides/).

---

## How it works

You can create custom functions or use any of the existing ones provided by Azion, both for **Edge Application** and **Edge Firewall**.

The language currently supported by the platform is JavaScript.

**Edge Functions** run during the handling of the request and Azion Edge Computing Platform provides a **Rules Engine** model that can trigger the execution of the Edge Functions code according to the handling phases.

The language-specific Runtime provides a programming interface for interacting and manipulating Request and Response objects to implement the necessary logic.

When instantiating an edge function, you can enter parameters that will be passed on to the function, in [JSON](https://www.json.org/) format, through arguments. You can also define and run tests online to validate its construction.

Edge Functions are performed directly on Azion Edge Infrastructure. To use them, they just need to be associated to a *Behavior* in the Rules Engine. Thus, when a request meets the criteria defined in the **Rule Engine** rules, the edge function will be triggered.

---

## Basics

You can create **Edge Functions** and maintain a repository of functions that can be used in **Edge Application** or **Edge Firewall**. Consult the [Runtime API](/en/documentation/products/edge-application/edge-functions/runtime-apis/javascript/) according to the Runtime chosen for writing the edge function.

In addition to customizing your own functions, you can also choose from the ready-to-use ones provided by Azion or Independent Software Vendors (ISV). Browse the [Azion Marketplace](/en/documentation/products/marketplace/) catalog on **Real-Time Manager (RTM)**.

### JavaScript Runtime Environment

By using the *JavaScript Runtime Environment*, Edge Functions written by the user go directly into effect without undergoing an internal review because the code runs on limited to isolated resources.

You can modify a function's behavior without changing the code itself. This means you don't need to hard-code the function. In the *Arguments (Args)* tab, you can insert `JSON` parameters by internal code functions. This format allows you to designate variable alternatives to your code that can contain details about a function and request.

*Arguments* are dynamic values that can change the Edge Functions running at the *edge nodes*.

You can use the same function in different Edge Applications.

For example, if you build an edge function with an argument that controls whether the code needs to send data to *Amazon S3 bucket*, and in a particular edge application you determine `true`, at the *Functions Instance*, in the *Args*, the function will generate a post for an S3 so the results of the request are kept.

- **Structure**: arguments are always `JSON` structures that will be stored in a function configuration through the *Args* tab in the functions module.
- **Instantiating**: in order to instantiate Args, use `event.args.<ARG_CREATED>`. By using this command you will be able to connect to the Args tab to your code. See our [examples page](/en/documentation/products/edge-application/edge-functions/javascript-examples/using-args/).

### Edge Functions Instances

According to its initiator type, before associating an execution trigger with Edge Function, it must be instantiated in Edge Application or Edge Firewall. With the Edge Functions module enabled, you can instantiate your edge functions for later use in a **Rules Engine Rule**, through the **Functions** tab.

Learn more about **Edge Functions Instances** in the [Edge Application](/documentation/products/edge-application/edge-functions-instances/) and [Edge Firewall](/documentation/products/edge-application/edge-functions-instances/) documentation.

---

## Activating your Settings

You will find the following buttons at the bottom of the screen:

- **Active:** this option enables or disables your settings on the system.
- **Cancel:** with this option, you return to the  Edge Functions home page, also discard your edits.
- **Save:** once your selections are complete, click on **Save** to save your settings.

When you save your settings, you return to the **Edge Functions** home page, where you see your list of Edge Functions sorted by these options: *name*, *language*, *initiator type*, *last editor*, *last modified,* *ref. count*, and *active*. By clicking on the arrows on those tabs, you can also change how your list is displayed.
