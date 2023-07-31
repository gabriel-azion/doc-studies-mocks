# Edge Functions for Edge Applications

Azion Edge Functions allows you to create event-driven, serverless applications, at the edge of the network, closer to users.

With Edge Functions, you can instantiate edge functions in your edge applications and execute them in response to events on edge nodes of our network with no need of having or managing servers.

With Edge Functions for Edge Applications, you can:

- Implement the required logic
- Reuse an edge function in different edge applications
- Keep and retrieve your pre-configured environment variables
- Access databases
- Write your code in JavaScript
- Deploy them easily
- Make use of pair programming with the Chat GPT integration
- Preview the outcome of the function live, on the preview deployment

---

## Implementation

| Scope | Guide |
| - | - | 
| WebAssembly | [How to create an edge function using WebAssembly on the Azion Edge platform](/en/documentation/products/guides/webassembly-on-azion-platform/) |
| Examples | [Examples](https://fun-cranberry.cloudvent.net/en/documentation/products/edge-application/edge-functions/javascript-examples/) |
| Code samples | [GitHub repository](https://github.com/aziontech/azion-samples/tree/dev/samples) |

---

## JavaScript Support

By using JavaScript in Edge Functions, you can execute code closer to the end user, enhancing performance and enabling custom logic for handling requests and responses.

Using the [Azion Edge Runtime](/en/documentation/products/edge-application/edge-functions/runtime/overview/) to develop your edge functions, you have a set of tools that help you implement your logic, such as:

- [Web standards APIs](/en/documentation/products/edge-application/edge-functions/runtime-apis/javascript/).
- [Metadata](/en/documentation/products/edge-application/edge-functions/runtime/api-reference/metadata/).
- [Network List method](/en/documentation/products/edge-application/edge-functions/runtime/api-reference/network-list/).
- [Environment Variables API](/en/documentation/products/edge-application/edge-functions/runtime/api-reference/environment-variables/)

---

### Next.js

Next.js is a JavaScript framework built on top of React that enables server-side rendering (SSR) and static site generation for building **Jamstack** applications.

**Jamstack**
Jamstack stands for JavaScript, APIs, and Markup, and it promotes decoupling the front end from the back end by pre-rendering content and serving it as static files.

**SSR**
SSR allows rendering React components on the server before sending them to the client, enhancing initial load times and improving SEO.

**Static Site**
Static site generation generates static HTML files at build time, which can be cached and delivered quickly to users, reducing the need for server-side processing.

---

## Function Instantiation



The **Edge Functions instances** module allows you to instantiate serverless functions in your edge applications, as well as set up conditions for their execution.

Once your edge application runs an edge function, it responds to events closer to the end user, ensuring greater scalability and availability.

Learn more about edge functions instances:

- [Edge Functions Instances](https://www.azion.com/en/documentation/products/edge-application/edge-functions-instances/)

---

## Rules Engine

Rules Engine handles the conditional execution of behaviors through logical operators. By using Rules Engine, you can build an architecture that provides better performance to your users while consuming fewer resources by processing at the origin.

Learn more about Rules Engine:

- [Rules Engine](https://www.azion.com/en/documentation/products/edge-application/edge-functions-instances/)

---

## Code Editor

The code editor for Edge Functions is the best way to get started developing your edge functions on the Azion platform. It's a web-based code editor that makes it easier and more intuitive to develop at the edge of the network. It's empowered by the Monaco Code Editor, used in VS Code, so if you're used to VS Code, you'll get familiar with it right away.

Some of its key features are:

- Syntax Highlighting.
- Intellisense.
- Debugging

[Learn more about the Edge Functions Code Editor](/en/documentation/products/edge-application/edge-functions/runtime-api/code-editor/).

---

## AI Assistant

Generative AI can be used in almost all tasks that involve understanding or generating natural language or code. In the development environment, it's a tool used for boosting developers' productivity.

In the edge functions scenario, it helps developers to:

- Debug code.
- Refactor code.
- Generate code based on prompts.

[Learn more about the AI Assistant](/en/documentation/products/edge-application/edge-functions/runtime-api/ai-integration/)

---

## Preview

You can check if the output is the expected with the Preview Deployment, making use of the `PreviewProvider` function, that emulates a request.

Learn more about [Preview Deployment](/en/documentation/products/edge-application/edge-functions/runtime-api/preview-deployment/)

---

## Debug

You can debug your edge functions in real-time using the `inspect` tool inside the [Preview Deployment](/en/documentation/products/edge-application/edge-functions/runtime-api/preview-deployment/) section.

You can also debug using:

- [Data Streaming](/en/documentation/products/guides/debugging-functions-data-streaming/)
- [GraphQL](/en/documentation/products/guides/debugging-functions-graphql/)

---
## Environment Variables

Environment variables are a crucial aspect of software development and deployment. They are used to store sensitive information or configuration settings that shouldn’t be hardcoded into the codebase.

Learn more about [Environment Variables](/en/documentation/products/edge-functions/environment-variables/)

---

## JSON Args

When you add JSON args, you can have different behaviors in your edge function without having to alter the code. Once you've set your json args, you can retrieve them by calling `event.args("desiredArg")`
