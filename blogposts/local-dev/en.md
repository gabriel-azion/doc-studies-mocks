
# Boost Software Quality: Local Development with Azion CLI

Azion CLI is an efficient tool for setting up local testing environments for edge functions. You can easily use it by executing the `azion dev` command, kickstarting the local development process.

For scenarios with edge firewall functions, you simply need to pass the `--firewall` flag alongside the command. This feature enriches your capabilities of testing and examining firewall functions before integrating them into the live product.

Key benefits:

-  *Error prevention*: test new features or modifications before they go live, reducing the risk of introducing mistakes to the production system.
-  *Improved debugging*: debug code more effectively and quickly in a controlled environment.
-  *Performance optimization*: test the application's behavior under different loads or unique user scenarios.
-  *Security enhancements*: identify and rectify security vulnerabilities before the application goes live.
-  *Development efficiency*: work without an internet connection, promoting productivity and autonomy.
-  *Cost-effective*: prevent high resource-consuming post-production fixes, saving time and money by addressing potential problems before deployment.

## Requirements

-   Azion CLI.
-   Node.js >= 18.

---

## Testing Edge Applications Functions

To kick off a local testing environment:

1.  Open the terminal, create a new directory, and access it.
2.  Initiate an application through azion init
3.  Name your application or accept the suggestion.
4.  Select JavaScript as the template.

> You can start the application based on the template you want. For this example, JavaScript is used.

5.  Start the local development by answering yes to the interaction.
6.  Install the dependencies.
7.  After a build process, Azion will return the port to access the application.
8.  Send requests to the server and check the behavior.

>note: you can always kill the terminal process and run `azion dev` to run the application locally. The changes applied to the function are rebuilt using hot reload.

The `azion dev` command starts up a local environment where you can test and monitor the functionality and efficiency of your edge functions.

Azion edge functions run on Azion Edge Runtime and have compatibility with Web APIs and Azion APIs.  

-   [Edge Functions First steps](https://www.google.com/url?q=https://www.azion.com/en/documentation/products/guides/edge-functions/first-steps/&sa=D&source=editors&ust=1712588650552049&usg=AOvVaw1kWgYzOGpycA85vtpm02Ww).
-   [Web APIs](https://www.google.com/url?q=https://www.azion.com/en/documentation/devtools/runtime-apis/javascript/&sa=D&source=editors&ust=1712588650552263&usg=AOvVaw0WMiVtGsSUX26WZxxGE295).
-   [Complete list of Azion Edge Runtime Web APIs suppor](https://www.google.com/url?q=https://www.azion.com/en/documentation/products/edge-application/edge-functions/runtime-apis/javascript/supported-types/&sa=D&source=editors&ust=1712588650552532&usg=AOvVaw0XRKfsyw5qA5WlWvBZQtbS)t.

---

## Testing Firewall Functions

If you've implemented firewall functions within your system, you'll need to consider special testing conditions.

To do so, you must run the `azion dev` command with the flag `--firewall`. It informs the system you're testing an edge firewall function.

-   [Edge function for Edge Firewall](https://www.google.com/url?q=https://www.azion.com/en/documentation/products/secure/edge-firewall/edge-functions/&sa=D&source=editors&ust=1712588650553124&usg=AOvVaw38iUKRhXJwa6Y4LoKn-ou9).
-   [Network List API](https://www.google.com/url?q=https://www.azion.com/en/documentation/products/edge-application/edge-functions/runtime/api-reference/network-list/&sa=D&source=editors&ust=1712588650553343&usg=AOvVaw2hcjn5aFnwuy9XPvrDNA1V).
-   [Metadata API](https://www.google.com/url?q=https://www.azion.com/en/documentation/products/edge-application/edge-functions/runtime/api-reference/metadata/&sa=D&source=editors&ust=1712588650553581&usg=AOvVaw2QZfrl8Gg-mF075fl3etLk).

---

## How Azion CLI Local Dev Works

### Dataflow

1.  Through Azion CLI, the user runs the `azion dev [flags]` command.
2.  Azion CLI invokes Vulcan, which manages build and local development.
3.  Vulcan initializes a server and this server instantiates the runtime. This runtime supports a list of [Web APIs](https://www.google.com/url?q=https://www.azion.com/en/documentation/devtools/runtime-apis/javascript/&sa=D&source=editors&ust=1712588650554220&usg=AOvVaw0TwWcXy_CpXvSQvex8y8gb) and emulates the actual [Azion Edge Runtime](https://www.google.com/url?q=https://www.azion.com/en/documentation/devtools/runtime/overview/&sa=D&source=editors&ust=1712588650554323&usg=AOvVaw3P6aay8XupL4d5pI8lnOp-).

### Responsibilities

Azion CLI: serves as the primary point of interaction between the user and the system. It manages the entire application deployment process, ensuring a smooth and efficient workflow.

Vulcan: the engine that drives project initialization, building, and adaptation. It intelligently tailors the project based on the selected template, ensuring that the application is optimally configured for its intended use. For local development, Vulcan:

-   Initiates a server.
-   Instantiates the Edge Runtime.
-   Handles changes in the source code, implementing hot reload.

---

## About Edge Functions

Azion Edge Functions are used to enhance edge applications or to boost security in an edge firewall. Both run on Azion Edge Runtime, reduce latency, and help to implement a distributed approach. OK, but what's the difference between them?

The difference is how the functions are structured, let's dive deeper into that.

### Edge Application Functions

First, edge functions for edge applications work based on a fetch event. They're initialized with an `addEventListener` function, passing fetch as the event type, and an event. For example:

```js 
addEventListener('fetch', event => {

      event.respondWith(handleRequest(event.request));

    });
```

Second, it’s necessary to define the behavior of the handleRequest function. This function has `event.request` as the signature. This data can be used later on to implement the necessary logic, such as:

-   Manipulate cookies.
-   Implement a behavior based on the HTTP request method (POST, GET, PUT, DELETE).
-   Access request metadata.

The `handleRequest` function can be defined as:

```js
 const html = `<!DOCTYPE html>

  <body>

    <h1>Hello World</h1>

    <p>This markup was generated by Azion - Edge Functions.</p>

  </body>`

  async function handleRequest(request) {

    return new Response(html, {

      headers: {

        "content-type": "text/html;charset=UTF-8",

      },

    })

  }
```

In this example, the response will be the HTML content, declared previously by the const html. The headers can be manipulated and, in the example, the content type is set.

Complete Example:

```js 
 const html = `<!DOCTYPE html>

  <body>

    <h1>Hello World</h1>

    <p>This markup was generated by Azion - Edge Functions.</p>

  </body>`

  async function handleRequest(request) {

    return new Response(html, {

      headers: {

        "content-type": "text/html;charset=UTF-8",

      },

    })

  }

  addEventListener('fetch', event => {

      event.respondWith(handleRequest(event.request));

    });
```

[Learn more about edge functions for edge applications](https://www.google.com/url?q=https://www.azion.com/en/documentation/products/guides/edge-functions/first-steps/&sa=D&source=editors&ust=1712588650561485&usg=AOvVaw0pkHrjh_COKU4FJbxrl0pP).

### Edge Firewall Functions

Edge functions for Edge Firewall operate based on a firewall event. They are initialized using the `addEventListener` function, passing `'firewall'` as the event type, and an event. For example:

```js
addEventListener('firewall', event => {

      event.deny();

  });

```

In this instance, the system sends a denial in response to the firewall event that has been triggered. There could be other event reactions like `event.continue()`, and `event.drop()` depending on the specific circumstances or logic desired.

It's necessary to define the potential behaviors for different event reactions within the firewall event listener. The exact response depends on the condition met. For example:

-   Detect threat levels.
-   Block or rights list IP addresses.
-   Implement behaviors based on traffic patterns.

An example where the `event.deny` function is defined and used:

```js
// Define a list of blocked IP addresses

  const blockedIPs = ["192.0.2.0", "203.0.113.0", "198.51.100.0"]

  addEventListener('firewall', event => {

      let ip = event.request.clientIP;

      if (blockedIPs.includes(ip)) {

          event.deny();

      } else {

          event.continue();

      }

  });
```

In this example, the firewall event listener checks the IP address that triggered the event against the list of blocked IPs. If the IP is on the list, the event is denied. If the IP isn't on the list, the event will continue processing. It showcases how you might use the `event.deny()`, `event.continue()`, and `event.drop()` in real application scenarios.

[Learn more about edge functions for edge firewall](https://www.google.com/url?q=https://www.azion.com/en/documentation/products/secure/edge-firewall/edge-functions/&sa=D&source=editors&ust=1712588650565018&usg=AOvVaw11pbsiwrO0Cs8vCuSNyMNi).

---

## Conclusion

Using local testing environments improves the product development process. Leveraging tools like Azion CLI makes it easier to build reliable, efficient, secure, and high-performing software solutions. By testing edge functions with the command `azion dev`, and optionally adding a `--firewall` flag when necessary, developers can navigate potential pitfalls before pushing their code into production.
