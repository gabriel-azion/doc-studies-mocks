# Vulcan 

[Vulcan](https://github.com/aziontech/vulcan) is a powerful, **open-source** tool designed to streamline the development and deployment of JavaScript applications and frameworks. This powerful **framework adapter** automates [polyfills]() for Edge Computing, significantly simplifying the process of creating Workers, particularly for the Azion platform.

## How Vulcan works

```mermaid
flowchart LR

A[Trigger] -->|args| B(Dispatcher)
B --> C(Prebuild)
C -->|args| D(Common Build)
D --> E[Artifacts]
```

### Components

| Step            | Description                                                                                                  | Responsibility                                                                                                                                                                     |
| -| - | - |
| **Trigger**     | An external call initiates the build process.                                                                 | Initiates the build process and triggers the Dispatcher.                                                                                                                            |
| **Dispatcher**  | Receives build options, selects the appropriate build process, and loads necessary template files and modules. | Decides which build process to run, imports required modules, and sets up the environment for further processing.                                                                  |
| **Prebuild**    | Custom prebuild module that generates the entrypoint and necessary files.                                      | Executes user-defined actions to prepare the environment for the main build process. All actions must be called in an exported default function.                                   |
| **Common Build**| Module that runs the Azion common build.                                                                      | Executes the Azion common build process. Polyfills may be used to generate worker files. Some configurable options can be passed to the builder, but attempting to override Azion worker configs will result in ignoring the passed configs. |
| **Artifacts**   | Generates the necessary files and folders for deployment on the Azion infrastructure.                          | Creates the '.edge' folder, which represents the edge locally. Generated files include: JS worker(s): '.edge/workers.js', Assets: '.edge/storage/*', Environment variables: '.edge/.env'                       |

---

## Installation

For quick integration into your project:

```bash
npm install edge-functions
```

or using Yarn:

```bash
yarn add edge-functions
```

---

## Development

1. **Clone the Repository:**

   ```bash
   git clone https://github.com/aziontech/vulcan.git
   ```

2. **Installation:**

   ```bash
   cd vulcan
   npm install
   npm install -g
   ```

3. **Start Developing:**

   Once installed, leverage Vulcan's capabilities to streamline your development workflow, including automated polyfills and Worker creation assistance.

## Using Vulcan

### Examples

1. **Build a JavaScript/Node project (back-end):**

   ```bash
   vulcan build
   ```

2. **Build a TypeScript/Node project (back-end):**

   ```bash
   vulcan build --preset typescript
   ```

3. **Build a Static Next.js project:**

   ```bash
   vulcan build --preset next --mode deliver
   ```

4. **Build a Static Astro.js project:**

   ```bash
   vulcan build --preset astro --mode deliver
   ```

5. **Test your project locally (after build):**

   ```bash
   vulcan dev
   ```

### Vulcan.config.js

The `vulcan.config.js` file serves as a powerful configuration system for Vulcan, offering customization options for your application's build process. While not mandatory, this file acts as an override mechanism, allowing you to define properties that supersede preset configurations. Unspecified properties will default to preset values.

->**Go to vulcan.config.js file reference documentation**->
