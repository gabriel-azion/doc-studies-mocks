# Enhancing Edge Functions Debugging with Azion logs

Live tail logs provide real-time insights into application behavior. However, accessing these logs can sometimes be complex. 

Azion CLI enables the watch of logs trough the terminal where you can check your edge functions' logs and your edge applications' logs.

The `azion logs cells` command offers the ability to watch your edge functions' `console.logs()` on your local machine, dramatically changing how you test and debug serverless functions, while the `azion logs http` command brings the HTTP logs related to your edge applications.

[Learn more about Edge Functions]()
[Learn more about Edge Applications]()


---

## Prerequisites for Using Azion CLI

- [Azion CLI installed](https://www.azion.com/en/documentation/products/azion-cli/overview/#installing-azion-cli).
- Node.js ≥ 18.
- Access to the command line.

---

## Behind The Scenes: How Azion CLI live tail logs Work

### Azion logs

![Azion logs](./logs.png "Azion logs")

#### Dataflow

1. The user initiates the process by executing the command `azion logs [ cells || http ]`.
2. The Azion CLI interacts with the GraphQL API.
3. The GraphQL API responds by returning logs from the last five minutes.
4. The CLI processes and interprets this data.
5. The logs are then presented to the user, with an option to display the data in a more readable, beautified format.

### Azion logs with live tail 

![Azion live tail logs](./live-tail.png "Azion live tail logs")

#### Dataflow

1. The user initiates the process by running the command `azion logs [ cells || http ] --tail`.
2. The Azion CLI then continuously calls the GraphQL API, each time starting from the timestamp of the last log that was displayed on the screen.
3. The GraphQL API responds by returning the requested data.
4. The CLI then processes and interprets this data.
5. Finally, the logs are returned to the user. The user has the option to receive this data in a more readable, beautified format.

### Responsibilities

**Azion CLI**: serves as the interface for user interaction and is responsible for formatting and returning the data to the user.

**GraphQL API**  handles the incoming requests (communicates with beholder) and retrieves the requested data.

---

## Putting It into Practice: Checking edge functions logs

### Checking logs locally

1.  Open your terminal.
2.  Run `azion init`.
3.  Choose the JavaScript template.
4.  Decide to run it locally.
5.  Install the dependencies.
6.  Edit the `main.js` file, created by the init command. Add `console.log()` statements as needed. Sample log statements to use for inspecting the request data:

```js
export default function myWorker(event) {
  // Log the event Request URL
  console.log("Request URL: ", event.request.url);
  // Log the event Request method
  console.log("Request Method: ", event.request.method);
  // Log the event Request headers
  console.log("Request Headers: ", event.request.headers);
  // If event.request.method is 'POST' or 'PUT', log the request body as well
  // Be aware: reading the body will consume it, so it will not be available for fetching anymore
  if (["POST", "PUT"].includes(event.request.method)) {
    event.request
      .clone()
      .text()
      .then((bodyText) => {
        console.log("Request Body: ", bodyText);
      });
  }
  return new Response("Hello, World");
}
```

7.  Run `azion dev`.
8.  Access the port provided at the end of the `azion dev` command's execution:
    - Run: curl http://localhost:{{port}}.
    - Visit: http://localhost:{{port}} in your browser.
9.  Check the generated logs in the terminal when the function executes.

### Deploying your application and checking live tail logs on the Azion Edge Platform

Follow these steps:

1.  Run `azion deploy` to deploy your application to the network edge.
2.  Access your application's domain, provided at the end of the deployment process.
3.  Run `azion logs cells --tail` to retrieve live tail logs of your edge functions.

> Note: the `azion logs cells` command fetches logs from the last 5 minutes. More details are available in the [command documentation](https://www.azion.com/en/documentation/products/azion-cli/overview/#using-azion-logs-cells).

---

## Harnessing Azion logs

The `azion logs cells` command provides direct access to essential debugging information. With mindfully structured logging of your serverless functions, you can gain insights into the sequence of operations, which simplifies spotting issues. Log statuses, error messages, function-specific data, inputs, outputs, and the application's state can expedite the debugging process.

## Benefits of Localized Console Logs

Localized console logs have several benefits:

- **Improved debugging**: Bringing edge-like conditions to your local setup enables efficient debugging, significantly reducing development time.
- **Better understanding of function behavior**: You can monitor the functionality and logic of your function in real time.
- **Iterative development**: Localized console logs simplify testing for iterative development cycles, ensuring each change operates as intended.
- **Decreased server costs**: Reducing server deployments for minute changes can lower server usage and expenses.

---

## Conclusion

[Azion CLI](https://www.azion.com/en/documentation/products/azion-cli/overview/) and Vulcan vastly simplify the development process, offering a comprehensive debugging tool via localized console logs for edge functions in local environments. Deploying your code on a server for each change is no longer necessary.

The `azion logs cells` command provides real-time function behaviour monitoring, which reduces both development time and server usage costs. Using these tools optimizes your code locally, saving early-stage development time, resources, and debugging effort.

By emulating edge-like conditions in your local environment, Azion reinforces the concept of the edge being ubiquitous. Begin using these tools today and upgrade to a seamless edge function development process. Let Azion bring the edge closer to you.
