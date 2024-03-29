---
title: Build with Hexo
description: Build with Heco.
meta_tags: hexo, js, jamstack
namespace: docs_framework_hexo
permalink: /documentation/products/build/frameworks-guides/hexo
---

Hexo is an open-source static site generator (SSG) that is designed to simplify the process of creating and managing websites or blogs. Static site generators like Hexo take a different approach to website development compared to traditional content management systems (CMS) like WordPress or dynamic web frameworks like Ruby on Rails.

Here are some key characteristics and features of Hexo:

- Static Site Generation

- Markdown Support

- Themes

- Plugin System

- Command-Line Interface (CLI)

- Git Integration

- Localization

Hexo is listed on [the Jamstack documentation](https://jamstack.org/generators/hexo/) as a static site generator, aligned to the Jamstack approach.

Learn more about [Hexo](https://hexo.io/docs/).

---

## Requirements

Before getting started, it's necessary to have:

- An Azion platform account with Edge Functions enabled.
- [The latest version of Azion CLI installed](/en/documentation/products/cli/overview/).
- Code editor.
- Access to the terminal.

---

## Initializing an Hexo project on the edge

Now, it's time to initialize a hexo project using the Azion CLI.

1. Initialize the project:

```sh 
  azion init
```

2. Accept the suggested name to your project, or enter the name you choose:

```sh 
(Hit enter to accept the suggested name in parentheses) Your project's name:  (dynamic_caligari)
```

Output: 

```sh
Getting modes available
```

3. Choose the Hexo template:

```sh 
Getting modes available? Choose a template for your project: (Use arrow keys)
  Angular 
 ❯Astro 
  Hexo 
  Next 
  React 
  Vue 
  Vite 
```

Now, Hexo's CLI will follow the process and initialize your Hexo project.

4. After the initialization is complete, choose the mode:

```sh 
Choose a mode:  [Use arrows to move, type to filter]
  Javascript (Compute)
  Typescript (Compute)
  Angular (Deliver)
  Astro (Deliver)
 >Hexo (Deliver)
  Next (Deliver)
  React (Deliver)
```

5. With the template fetched and configured, you can now start a local development server or not.

```sh 
Do you want to start a local development server? (y/N) 
```

The following steps are based on the answer you gave. 

- [If you chose to have a local development server running]().
- [If you chose not to have a local development server running]().

### Answering yes to local dev

1. Install the project dependencies. Input `y` when the interaction prompts:

```sh 
  Do you want to install project dependencies? This may be required to start local development server (y/N)
```

Wait until the installation is complete.

Output

```sh
Your Edge Application was built successfully
[Vulcan] [Server] › ✔  success   Function running on port http://localhost:3000/
```

2. On the browser, go to `http://localhost:3000/`, and you can now see your Hexo Project running: 

#### Deploying the project

When your project is running locally, you are still able to deploy it to the edge, to do so: 

1. Stop the terminal execution with `control + c`.

2. Access the project folder:

```sh
cd [your-project-name] 
```

3. Deploy the project:

```sh
azion deploy
```

4. Wait while the project is built and deployed to the Azion edge platform.


After the deployment is complete, you'll receive a domain for accessing your Hexo project on the Azion Platform.

Wait a few minutes so the propagation takes place, and then access your application using the provided domain, which should be similar to:

https://xxxxxxx.map.azionedge.net


### Answering no to local dev

Now, after indicating you don't want to have a local server running, let's deploy the Hexo project to the edge. 

1. Enter `y` to the following interaction, indicating you want to deploy the project:

```sh
   Do you want to deploy your project? (y/N) 
```

2. Install the project dependencies. Input `y` when the interaction prompts:

```sh 
  Do you want to install project dependencies? This may be required to deploy your project (y/N)
```

3. Wait while the project is built and deployed to the Azion edge platform.


After the deployment is complete, you'll receive a domain for accessing your Hexo project on the Azion Platform.

Wait a few minutes so the propagation takes place, and then access your application using the provided domain, which should be similar to:

https://xxxxxxx.map.azionedge.net