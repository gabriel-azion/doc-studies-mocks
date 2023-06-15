---
layout: page-documentation-md
title: How to Build and Publish a Next.js Project with SSR on the Azion Platform
description: Next.js, a flexible framework based on the React library, provides powerful tools for building fast applications. SSR generates HTML for each request, offering several benefits 
meta_tags: javascript, edge computing, Next.js
namespace: docs_use_case_nextJS
permalink: "/documentation/products/guides/nextjs-on-azion-platform/"
permalink_pt-br: "/documentacao/produtos/guias/nextjs-na-plataforma-azion/"
---

# How to Build and Publish a Next.js Project with Server-side Rendering (SSR) on the Azion Platform

## Next.js and Server-side Rendering (SSR)

**Next.js**, a flexible framework based on the **React** library, provides powerful tools for building fast applications.

**SSR** generates HTML for each request, offering several benefits, including:

- Improved initial loading performance
- Search engine optimization (SEO)
- Social media sharing
- Enhanced user experience
- Accessibility and compatibility
- Code sharing and performance optimizations

## Next.js SSR Project on the Azion Platform

### Requirements

Before getting started, make sure you have:

- An Azion platform account with Edge Functions enabled
- Node.js runtime environment (version 16.x or 18.x) installed in your build environment
- The latest version of Azion CLI installed
- Next.js installed.

To install the Azion CLI, visit [Installing Azion CLI manually]({% tl documentation_how_to_cli_installing_manually %}) page.

> **Note**: currently, the supported Next.js version is `12`

### Setting up the Project

1. Create a new folder for your project:

```bash
  mkdir next-js-azion
```

2. Access the project folder:

```bash
  cd next-js-azion
```

3. Inside the project folder, use the following command to create a Next.js project:

```bash
  npx create-next-app@12 azion-next-ssr && cd azion-next-ssr && npm i next@12
```

4. Open the project directory in your preferred code editor (e.g., VSCode):

```bash
  code .
```

### Configuring Next.js for Azion

1. Open the `next.config.js` file in your project's root directory.

2. Add the `experimental` object inside the `nextConfig` constant:

```javascript
  const nextConfig = {
    experimental: {
      runtime: 'experimental-edge',
    },
    reactStrictMode: true,
    swcMinify: true,
  }
  module.exports = nextConfig
```

### Building and Publishing the Application on the Azion Platform

1. In the terminal, in your project's root directory, initialize the Azion Edge Application:

```bash
  azioncli edge_applications init
```

2. Run the `build` command:

```bash
  azioncli edge_applications build
```

3. Publish the application:

```bash
  azioncli edge_applications publish
```

After running the `publish` command, you will receive a domain for accessing your SSR Next.js project on the Azion Platform. 

Wait for a few minutes so the propagation takes place, and then access your application using the provided domain, that should be similar to:

`https://ala5yasjasdsa0pnm.map.azionedge.net`.

---

Didn't find what you were looking for? [Open a ticket](https://tickets.azion.com/).