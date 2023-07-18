---
title: Step-by-step creating an Edge Function
description: 
meta_tags:
namespace: 
permalink:
---

To see your **Edge Function** in effective operation you just need to write, instantiate, and associate it with a Behavior *Run Function*, using a Rule in the **Rules Engine**. 

1. Log into the [**RTM**](https://manager.azion.com/). On the *Products Menu*, click **Edge Functions**.
2. Click **Add Function** to add a new Edge Function.
3. Name your function in the **Edge Function Name** field to be able to save your settings.
4. In *Language*, select **JavaScript**. Copy the following example to the *Code* tab field.

```js
async function handleRequest(request) {
 return new Response("Hello World!",
   {
       status:200
   })
}
addEventListener("fetch", event => {
 event.respondWith(handleRequest(event.request))
})
```

1. In the *Function to run* field, enter the name of the main function to run in the source code.
2. Select the *Initiator Type*, which refers to the type of module where the function will be instantiated and executed.  In this example, it refers to **Edge Application**.
3. Click on **Save** to save your settings. You return to the Edge Functions home page, where you see your list of Edge Functions.
4. Then, access the **Products** menu, on the top left. Select an Edge Application from your list.
5. On the *Main Settings* tab, enable the Edge Functions module in the *Edge Application Modules* section.
6. On the *Rules Engine* tab, create or edit a Rule and in the *Behavior* section, in the *Then* field, select **Run Function** and associate it to the desired Edge Function.
7. Example of response when running the Behavior *Run Function*:

   `Hello World!`



1. Use **Real-Time Metrics** to check on your metrics. For example, when you want to see the number of *Invocations of Edge Functions instances*.

> Fields marked with an asterisk are required.

---