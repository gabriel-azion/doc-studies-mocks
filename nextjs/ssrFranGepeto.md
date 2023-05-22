# Guide: Building and Publishing a Next.js Project with Server-side Rendering (SSR) on the Azion Platform

## Introduction
When developing modern web applications, it's crucial to consider factors like interface, infrastructure, and performance. Next.js, a flexible framework based on the React JavaScript library, provides powerful tools for building fast web applications.

## Server-side Rendering (SSR)
SSR generates HTML for each request, offering several benefits, including:
- Improved initial loading performance
- Search engine optimization (SEO)
- Social media sharing
- Enhanced user experience
- Accessibility and compatibility
- Code sharing and performance optimizations

## Next.js SSR Project on the Azion Platform

### Requirements
Before getting started, ensure you have the following:
- An Azion platform account with Edge Functions enabled.
- Node.js runtime environment (version 16.x or higher) installed in your build environment.
- The latest version of Azion CLI installed.

### Setting up the Project
1. Create a new folder for your project:

```
  mkdir next-js-azion
```

2. Access the project folder:

```
  cd next-js-azion
```

3. Inside the project folder, use the following command to create a Next.js project:

```
  npx create-next-app@12 <azion-next-ssr> && cd <azion-next-ssr> && npm i next@12
```

4. Open the project directory in your preferred code editor (e.g., VSCode):

```
  code .
```

### Configuring Next.js for Azion

1. Open the `next.config.js` file in your project's root directory.

2. Add the following configuration inside the `nextConfig` constant:

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

1. In the terminal, located in your project's root directory, initialize the Azion Edge Application:

```
  azioncli edge_applications init
```

2. Run the build command:

```
  azioncli edge_applications build
```

3. Publish the application:

```
  azioncli edge_applications publish
```

After running the publish command, you will receive a domain for accessing your SSR Next.js project on the Azion Platform. Wait for a few minutes to allow for propagation, and then access your application using the provided domain (e.g., https://ala5yasjasdsa0pnm.map.azionedge.net).

---

Didn't find what you were looking for? [Open a ticket](https://tickets.azion.com/).
