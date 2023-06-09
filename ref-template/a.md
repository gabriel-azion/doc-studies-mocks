# Edge Functions

Azion Edge Functions allows you to create event-driven, serverless applications, at the edge of the network, closer to users.

With Edge Functions, you can perform serverless functions in response to events on edge nodes of our network with no need of having or managing servers.

![imagem como o Edge Functions funciona](./arch.png)

[Find out more about how to get started with Edge Functions](...)

## Capabilities

### JavaScript Support

JavaScript is a popular programming language used for web development, enabling dynamic and interactive website features. It runs on the client-side and is supported by all major web browsers. By using JavaScript in Edge functions, you can execute code closer to the end user, enhancing performance and enabling custom logic for handling requests and responses.

Using the Azion Edge Runtime to develop your own edge functions, you have a set of tools that help you implement your logic, such as:

- [Web standards APIs](https://www.azion.com/en/documentation/products/edge-application/edge-functions/runtime-apis/javascript/).
- [Metadata](https://www.azion.com/en/documentation/products/edge-application/edge-functions/runtime/api-reference/metadata/).
- [Network List method](https://www.azion.com/en/documentation/products/edge-application/edge-functions/runtime/api-reference/network-list/).

### Javascript frameworks support
>It has a dedicated page

#### Next.js

Next.js is a JavaScript framework built on top of React that enables server-side rendering (SSR) and static site generation for building **Jamstack** applications.

**Jamstack**
Jamstack stands for JavaScript, APIs, and Markup, and it promotes decoupling the front-end from the back-end by pre-rendering content and serving it as static files.

**SSR**
SSR allows rendering React components on the server before sending them to the client, enhancing initial load times and improving SEO.

**Static Site**
Static site generation generates static HTML files at build time, which can be cached and delivered quickly to users, reducing the need for server-side processing.

### Function Instantiation
> // Deserves a dedicated page, currently we have two pages, one for firewall and another one for applications 
[Application](https://www.azion.com/en/documentation/products/edge-application/edge-functions-instances/)
[Firewall](https://www.azion.com/en/documentation/products/edge-firewall/edge-functions-instances/)

The Edge Functions module allows you to instantiate serverless functions in your edge applications and edge firewall, as well as set up conditions for its execution.

Once your edge application or edge firewall runs edge functions, it responds to events closer to the end user, ensuring greater scalability and availability.

Learn more about edge functions instances:

- [Application](https://www.azion.com/en/documentation/products/edge-application/edge-functions-instances/)
- [Firewall](https://www.azion.com/en/documentation/products/edge-firewall/edge-functions-instances/)


### Rules Engine

Rules Engine is a capability that handles the conditional execution of behaviors through logical operators. By using Rules Engine, you can build an architecture that provides better performance to your users while consuming fewer resources by processing at the origin.

Available for Edge Application and Edge Firewall.

Learn more about Rules Engine: 

- [Application](https://www.azion.com/en/documentation/products/edge-application/edge-functions-instances/)
- [Firewall](https://www.azion.com/en/documentation/products/edge-firewall/edge-functions-instances/)

### Code editor

The new code editor for Edge Functions is the best way to get started developing your edge functions on the Azion platform. It's a web-based code editor that makes it easier and more intuitive to develop at the edge of the network. It's empowered by the Monaco Code Editor, used in VS Code, so if you're used to VS Code, you'll get familiar with it right away.

Some of its key features are:

- Syntax Highlighting.
- Intellisense.
- Debugging

[Learn more about the Edge Functions Code Editor](https://www.azion.com/en/documentation/products/edge-application/edge-functions/runtime-api/code-editor/).

### AI Assistant

Generative AI can be used in almost all tasks that involve understanding or generating natural language or code. In the development environment, it's a tool used for boosting developers productivity.

In the edge functions scenario, it helps developers to:

- Debug code.
- Refactor code.
- Generate code based on prompts.

[Learn more about the AI Assistant](https://www.azion.com/en/documentation/products/edge-application/edge-functions/runtime-api/ai-integration/)

---

## Creating an edge function

You can create your own edge functions in JavaScript with the help of an AI tool and have your function preview presented to you on real-time. To do so, you need to write or copy and paste your JavaScript code, following the required structured to have it running on the Azion Edge Platform.

## Adding JSON args

When you add json args, you can have different behaviors in your edge function without having to alter the code. Once you've set your json args, you can retrieve them by calling `event.args("desiredArg")`

## Previewing

You can check if the output is the one expected with the Preview Deployment, making use of the `PreviewProvider` function, that emulates a request.

## Debugging

You can debug your edge functions on real time using the `inspect` tool inside the [Preview Deployment](https://www.azion.com/en/documentation/products/edge-application/edge-functions/runtime-api/preview-deployment/) section.

You can also debug using:

- [Data Streaming]()
- [Real-time Metrics]()
- [GraphQL]()

--- 
## Run a function

Once you've created your edge function, you can configure a rule in Rules Engine and set the behavior to be `Run a function`, then, based on the rule configured, your edge application or edge firewall will run the chosen function.

---

## Limits

| Where | Developer | Enterprise | Mission Critical| 
| - | - | - | - |
| Arguments | 100kb | 100kb | 100kb |
| Memory per Isolate | 512mb | 512mb | 512mb |
| Arguments | 100kb | 100kb | 100kb |
| Arguments | 100kb | 100kb | 100kb |
---

Didn't find what you were looking for? Open a support ticket.
