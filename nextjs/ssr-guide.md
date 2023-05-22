---
layout: page-documentation-md
title: Creating a Function using Next.js on Azion's platform 
description: When building a modern application, there are a few things to take into consideration, such as interface, infrastructure, performance, and so forth. Next.js is a flexible framework based on the React JavaScript library that provides tools for building fast web applications. 
meta_tags: javascript, edge computing, Next.js
namespace: docs_use_case_nextJS
permalink: "/documentation/products/guides/nextjs-on-azion-platform/"
permalink_pt-br: "/documentacao/produtos/guias/nextjs-na-plataforma-azion/"
---

# How to build and publish a Next.js project with SSR on the Azion platform

When building a modern application, there are some issues to consider such as interface, infrastructure, performance, and so on. The **Next.js** framework is a flexible structure based on **React** JavaScript library that provides tools for building fast web applications.

Visit the [React](https://reactjs.org/) library and [Next.js](https://nextjs.org/) framework sites for more information.

## Server-side Rendering
A page that uses Server-side Rendering (SSR), has its html generated on each request.

SSR offers a list of benefits, such as:

- Improved initial loading performance.
- Search engine optimization (SEO).
- Social media sharing.
- Enhanced user experience.
- Accessibility and compatibility.
- Code sharing and performance optimizations.

## Prerequisites

To create a Next.js application with SSR on the Azion platform, you need:

- An account on the Azion platform with **Edge Functions** enabled.
- The **Node.js** runtime environment, version 16.x or higher, installed in a *build* environment.
- The latest **Azion CLI** version installed.
- Next.js on the Version 12

To install the Azion CLI, visit its [reference documentation]({% tl documentation_CLI %}) page.

1. Create a folder with the name of the project:

```bash
    mkdir next-js-azion
```

2. Access the recently created folder:

```bash
    cd next-js-azion
```

3. With the `next-js-azion` folder in the terminal, run the following command to create a Next.js project:

```bash
    npx create-next-app@12 <azion-next-ssr> && cd <azion-next-ssr> && npm i next@12
```

4. Open the current directory on VScode:

```bash
    code .
```

5. Go to the file named `next.config.js` and paste this configuration inside the `nextConfig` constant:

```bash
    experimental: {
    runtime: 'experimental-edge',
    }
```

The `next.config.js` file should look like this:

```bash
    const nextConfig = {
    experimental: {
        runtime: 'experimental-edge',
    },  
    reactStrictMode: true,
    swcMinify: true,
    }

    module.exports = nextConfig
```

6. On your project's root directory, open the terminal and run:

```bash
    azioncli edge_applications init
```


7. Run the build command: 

```bash
    azioncli edge_applications build
```

8. Then, publish the application: 

```bash
    azioncli edge_applications publish
```

The expected output should look like:

```bash
    Building your Edge Application. This process may take a few minutes

    Your Edge Application was built successfully

    Uploading static files
    [##########] 100.00% .vercel/output/static/vercel.svg Upload completed successfully!

    Created Edge Function azion-next-ssr with ID 0

    Created Edge Application azion-next-ssr with ID 0

    Created Domain azion-next-ssr with ID 0

    Your Edge Application was published successfully

    To visualize your application access the domain: https://xxxxxxx.map.azionedge.net
```
After the `publish` command, you'll get a domain, such as:

```bash
    https://ala5yasjasdsa0pnm.map.azionedge.net
```

Wait a few minutes so the propagation takes place and access your ssr Next.js project on the Azion Platform.

---

Didn't find what you were looking for? [Open a ticket](https://tickets.azion.com/).
