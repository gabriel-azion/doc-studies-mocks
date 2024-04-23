# Enhancing Edge Functions Debugging with Azion logs

This blog post will guide you through the nuances of managing logs for edge functions, providing valuable insights and techniques to streamline development and master debugging.

Using [Azion CLI](https://www.azion.com/en/documentation/products/azion-cli/overview/), you can initiate, run, and inspect edge functions' logs through the following commands:

- `azion init`: Initializes the application.
- `azion dev`: Runs your application locally.
- `azion deploy`: Deploys your application on Azion's distributed Edge Network.
- `azion logs cells`: Observes the logs inside the function's code running at the edge of the network.

The `azion logs cells` command offers the ability to view console logs on your local machine, dramatically changing how you test and debug serverless functions.

## Putting It into Practice: Checking Request Data

### Requirements

Before starting this implementation, ensure that you have:

- [Azion CLI installed](https://www.azion.com/en/documentation/products/azion-cli/overview/#installing-azion-cli).
- Node.js ≥ 18.x.y

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

### Deploying your application and checking logs on the Azion Edge Platform

Follow these steps:

1.  Run `azion deploy` to deploy your application to the network edge.
2.  Access your application's domain, provided at the end of the deployment process.
3.  Run `azion logs cells` to retrieve logs of your edge functions.

> Note: the `azion logs cells` command fetches logs from the last 5 minutes. More details are available in the [command documentation](https://www.azion.com/en/documentation/products/azion-cli/overview/#using-azion-logs-cells).

## Harnessing Azion logs

The `azion logs cells` command provides direct access to essential debugging information. With mindfully structured logging of your serverless functions, you can gain insights into the sequence of operations, which simplifies spotting issues. Log statuses, error messages, function-specific data, inputs, outputs, and the application's state can expedite the debugging process.

## Benefits of Localized Console Logs

Localized console logs have several benefits:

- **Improved debugging**: Bringing edge-like conditions to your local setup enables efficient debugging, significantly reducing development time.
- **Better understanding of function behavior**: You can monitor the functionality and logic of your function in real time.
- **Iterative development**: Localized console logs simplify testing for iterative development cycles, ensuring each change operates as intended.
- **Decreased server costs**: Reducing server deployments for minute changes can lower server usage and expenses.

## Conclusion

[Azion CLI](https://www.azion.com/en/documentation/products/azion-cli/overview/) and Vulcan vastly simplify the development process, offering a comprehensive debugging tool via localized console logs for edge functions in local environments. Deploying your code on a server for each change is no longer necessary.

The `azion logs cells` command provides real-time function behaviour monitoring, which reduces both development time and server usage costs. Using these tools optimizes your code locally, saving early-stage development time, resources, and debugging effort.

By emulating edge-like conditions in your local environment, Azion reinforces the concept of the edge being ubiquitous. Begin using these tools today and upgrade to a seamless edge function development process. Let Azion bring the edge closer to you.
