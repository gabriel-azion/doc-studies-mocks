---
title: Build with Astro
description: Build with Astro.
meta_tags: astro, js, jamstack
namespace: docs_framework_astro
permalink: /documentation/products/build/frameworks-astro/
---

Astro is an open-source web framework designed with an emphasis on speed and suitability for websites that contain substantial content, such as:

- Landing pages
- Blogs
- Technical documentation
- Similar types of online platforms

Astro is listed on [the Jamstack documentation](https://jamstack.org/generators/astro/) as a static site generator, aligned to the Jamstack approach.

Learn more about [Astro](https://docs.astro.build/en/getting-started/).

---

## Requirements

Before getting started, it's necessary to have:

- An Azion platform account with Edge Functions enabled.
- [The latest version of Azion CLI installed](/en/documentation/products/cli/overview/).
- Code editor.
- Access to the terminal.

---

## Initializing an Astro project on the edge

Now, you've created an Astro project and it's time to deploy it to the Azion nodes.

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

3. Choose the Astro template: 

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

Now, Astro's CLI will follow the process and initialize your Astro project.

4. After the initialization is complete, choose the mode:

```sh 
Choose a mode:  [Use arrows to move, type to filter]
  Javascript (Compute)
  Typescript (Compute)
  Angular (Deliver)
> Astro (Deliver)
  Hexo (Deliver)
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

2. On the browser, go to `http://localhost:3000/`, and you can now see your Astro Project running: 

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


After the deployment is complete, you'll receive a domain for accessing your Astro project on the Azion Platform.

Wait a few minutes so the propagation takes place, and then access your application using the provided domain, which should be similar to:

https://xxxxxxx.map.azionedge.net


### Answering no to local dev

Now, after indicating you don't want to have a local server running, let's deploy the Astro project to the edge. 

1. Enter `y` to the following interaction, indicating you want to deploy the project:

```sh
   Do you want to deploy your project? (y/N) 
```

2. Install the project dependencies. Input `y` when the interaction prompts:

```sh 
  Do you want to install project dependencies? This may be required to deploy your project (y/N)
```

3. Wait while the project is built and deployed to the Azion edge platform.


After the deployment is complete, you'll receive a domain for accessing your Astro project on the Azion Platform.

Wait a few minutes so the propagation takes place, and then access your application using the provided domain, which should be similar to:

https://xxxxxxx.map.azionedge.net