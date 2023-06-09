---
title: Story book
description: Azion web story book
meta_tags: story-book
permalink: documentation/story-book
---


## [Story Book](https://fun-cranberry.cloudvent.net/en/documentation/story-book)

### Spoiler 

import Spoiler from '~/components/Spoiler.astro';

<Spoiler>Linux</Spoiler>


## Buttom and Badge
### Badge

import Badge from '~/components/Badge.astro';

<Badge>
  Badge
</Badge>

<Badge variant="accent"> 
  Badge 
</Badge>

### Buttom

import Button from '~/components/Button.astro'

<Button href="/en/"> 
my button 
</Button>

## Alerts/Calls/Destak

### Bloquote
> meu texto com bloquote

### Note
:::note
Um [elemento `<slot />`](/pt-br/core-concepts/astro-components/#slots) dentro de um componente HTML irá funcionar assim como funcionaria em um componente Astro. Para utilizar o [Componente Web HTML Slot](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/slot) no lugar, adicione `is:inline` ao seu elemento `<slot>`.
:::

### Tip
:::tip
Os estilos definidos aqui se aplicam apenas ao conteúdo escrito diretamente no próprio template do componente. Filhos e componentes importados **não** serão estilizados por padrão.
:::


### Caution
:::caution
Os estilos definidos aqui se aplicam apenas ao conteúdo escrito diretamente no próprio template do componente. Filhos e componentes importados **não** serão estilizados por padrão.
:::

### Destaque

`<p>{operatingSystem}</p>`


## Terminal && Code Snippets

### Simple
```ini title=".env"
SECRET_PASSWORD=password123
PUBLIC_ANYBODY=there
```

```sh
npm install @astrojs/mdx
```

### Git Dffs

```astro ins={3-6} del={8}
---
// src/components/TituloSaudacao.astro
export interface Props {
  nome: string;
  saudacao?: string;
}

const { saudacao = "Olá", nome } = Astro.props;
---
<h2>{saudacao}, {nome}!</h2>
```

```astro title="src/components/MyComponent.astro" ".src" ".width" ".height" del={2,5} ins={3,6}
---
import rocket from '../images/rocket.svg';
import rocket from '../assets/images/rocket.svg'
---
<img src={rocket} width="250" height="250" alt="A rocketship in space." />
<img src={rocket.src} width={rocket.width} height={rocket.height} alt="A rocketship in space." />
```

```astro ins="= \"Olá\"" ins="= \"Astronauta\"" {1-4} 
---
// src/components/TituloSaudacao.astro
const { saudacao = "Olá", nome = "Astronauta" } = Astro.props;
---
<p>{saudacao}, {nome}!</p>
```

:::tip
Nossos snippets aceitam códigos de:
```
	code: ['astro', 'cjs', 'htm', 'html', 'js', 'jsx', 'mjs', 'svelte', 'ts', 'tsx', 'vue'],
	data: ['env', 'json', 'yaml', 'yml'],
	styles: ['css', 'less', 'sass', 'scss', 'styl', 'stylus'],
	textContent: ['markdown', 'md', 'mdx'],
  terminal: ['shellscript', 'shell', 'bash', 'sh', 'zsh']
```
:::

### Manager Tabs

import PackageManagerTabs from '~/components/tabs/PackageManagerTabs.astro'

<PackageManagerTabs>
    <Fragment slot="npm">
    ```shell
    npx astro add netlify
    ```
    </Fragment>
    <Fragment slot="pnpm">
    ```shell
    pnpm astro add netlify
    ```
    </Fragment>
    <Fragment slot="yarn">
    ```shell
    yarn astro add netlify
    ```
    </Fragment>
</PackageManagerTabs>

import AstroJSXTabs from '~/components/tabs/AstroJSXTabs.astro'

<AstroJSXTabs>
  <Fragment slot="jsx">
    ```jsx title="component.jsx"
    import * as React from "react"
    import { useStaticQuery, graphql } from "gatsby"
    import Header from "./header"
    import Footer from "./footer"
    import "./layout.css"

    const Component = ({ message, children }) => {
      const data = useStaticQuery(graphql`
        query SiteTitleQuery {
          site {
            siteMetadata {
              title
            }
          }
        }
      `)
      return (
        <>
          <Header siteTitle={data.site.siteMetadata.title} />
          <div style={{ margin: `0`, maxWidth: `960`}}>{message}</div>
          <main>{children}</main>
          <Footer siteTitle={data.site.siteMetadata} />
        </>
      )
    }

    export default Component
    ``` 
  </Fragment>
    <Fragment slot="astro">
    ```astro title="component.astro"
    ---
    import Header from "./Header.astro"
    import Footer from "./Footer.astro"
    import "../styles/stylesheet.css"
    import { site } from "../data/siteMetaData.js"
    const { message } = Astro.props
    ---
    <Header siteTitle={site.title} />
      <div style="margin: 0; max-width: 960;">{message}</div>
      <main>
        <slot />
      </main>
    <Footer siteTitle={site.title} />
    ```
  </Fragment>
</AstroJSXTabs>

:::tip
  Também há outros ocmponentes similares, como: 
  `<AstroVueTabs>`: Compara Astro com Vue em duas tabs
  `<JavascriptFlavorTabs>`: Compara TypeScript com JS em tabs
  `<StaticSsrTabs>`: Compara configs, em astro mesmo
  `UIFrameworkTabs`: Compara UI frameworks (React, Vue, etc)
:::

## File Tree

### Simple

import FileTree from '~/components/FileTree.astro'

<FileTree>
- public/
  - robots.txt
  - favicon.svg
  - social-image.png
- src/
  - components/
    - Header.astro
    - Button.jsx
  - layouts/
    - PostLayout.astro
  - pages/
    - posts/
      - post1.md
      - post2.md
      - post3.md
    - index.astro
  - styles/
    - global.css
- astro.config.mjs
- package.json
- tsconfig.json
</FileTree>

### Actived
<FileTree>
- src/pages/
  - _hidden-directory/
    - page1.md
    - page2.md
  - _hidden-page.astro
  - **index.astro**
  - posts/
    - _SomeComponent.astro
    - _utils.js
    - **post1.md**
</FileTree>

## Video

## Normal Video

import Video from '~/components/Video.astro';

<Video src="https://user-images.githubusercontent.com/4033662/197398760-8fd30eff-4d13-449d-a598-00a6a1ac4644.mp4" type="video/mp4" />
{/* https://www.npmjs.com/package/@astro-community/astro-embed-youtube */}


### Lopping Video 

import LoopingVideo from '~/components/LoopingVideo.astro'

<LoopingVideo sources={[{ src: '/videos/stores-example.mp4', type: 'video/mp4' }]} />

## Deploy Guides
import DeployGuidesNav from '~/components/DeployGuidesNav.astro';

<DeployGuidesNav />

## Box

import Box from '~/components/tutorial/Box.astro'
import Checklist from '~/components/Checklist.astro';
import MultipleChoice from '~/components/tutorial/MultipleChoice.astro';
import Option from '~/components/tutorial/Option.astro';

<Box icon="check-list">
## Checklist

<Checklist>
- [ ] I can create a new page for my website and link to it from an existing page.
- [ ] I can commit my changes back to GitHub and update my live site on Netlify.
</Checklist>
</Box>

<Box icon="puzzle-piece">
## Try it yourself - Add a Blog page

Add a third page `blog.astro` to your site, following the [same steps as above](#create-a-new-astro-file).

(Don't forget to add a third navigation link to every page.)

<details>
<summary>Show me the steps.</summary>
1. Create a new file at `src/pages/blog.astro`.
2. Copy the entire contents of `index.astro` and paste them into `blog.astro`.
3. [Add a third navigation link](#add-navigation-links) to the top of every page:

```astro title="src/pages/index.astro" ins={4}
<body>
  <a href="/">Home</a>
  <a href="/about/">About</a>
  <a href="/blog/">Blog</a>

  <h1>My Astro Site</h1>
</body>
```
</details>
</Box>

<Box icon="question-mark">

### Test your knowledge

Which of the following is...
1. A code editor, for making changes to your files and their content?

    <MultipleChoice>
      <Option>
        web browser
      </Option>
      <Option>
        Terminal
      </Option>
      <Option isCorrect>
        VS Code
      </Option>
    </MultipleChoice>

2. An online version control provider for your repository?

    <MultipleChoice>
      <Option isCorrect>
        GitHub
      </Option>
      <Option>
        Terminal
      </Option>
      <Option>
        VS Code
      </Option>
    </MultipleChoice>

3. An application for running commands?
    <MultipleChoice>
      <Option>
        GitHub
      </Option>
      <Option isCorrect>
        Terminal
      </Option>
      <Option>
        web browser
      </Option>
    </MultipleChoice>

</Box>


## Checks

import PreCheck from '~/components/tutorial/PreCheck.astro';

<PreCheck>
  - Install any tools that you will use to build your Astro website
</PreCheck>

import Lede from '~/components/tutorial/Lede.astro';

<Lede> In this tutorial, you'll learn Astro's key features by building a fully-functioning blog, from zero to full launch! 🚀 </Lede>

import DontEditWarning from '~/components/DontEditWarning.astro';

<DontEditWarning />

### Diagramas
import IslandsDiagram from '~/components/IslandsDiagram.astro';

<IslandsDiagram>
  <Fragment slot="headerApp">Header (interactive island)</Fragment>
  <Fragment slot="sidebarApp">Sidebar (static HTML)</Fragment>
  <Fragment slot="main">
    Static content like text, images, etc.
  </Fragment>
  <Fragment slot="carouselApp">Image carousel (interactive island)</Fragment>
  <Fragment slot="footer">Footer (static HTML)</Fragment>
  <Fragment slot="source">Source: [Islands Architecture: Jason Miller](https://jasonformat.com/islands-architecture/)</Fragment>
</IslandsDiagram>

:::tip 
  Só temos esse diagrama por enquanto e ele é focado no Astro, temos que editar caso o uso seja necessário
:::


import Since from '~/components/Since.astro'

<Since v="2.6.0" />

:::caution
  Precisa ser editado para ser utilizado
::: 

### Recipes 
import RecipeLinks from "~/components/RecipeLinks.astro"

<RecipeLinks slugs={["en/astro/recipes/i18n"]} />

import RecipesNav from '~/components/RecipesNav.astro';

<RecipesNav />

:::caution 
  O recipes nav só renderiza itens que são do tipo RECIPES
:::


### Contribuitors

import ContributorList from '~/components/ContributorList.astro'

<ContributorList githubRepo="withastro/docs" />
