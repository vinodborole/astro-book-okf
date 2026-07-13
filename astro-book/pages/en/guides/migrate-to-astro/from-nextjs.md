---
type: Web Page
title: Migrating from Next.js | Docs
description: Tips for migrating an existing Next.js project to Astro
resource: https://docs.astro.build/en/guides/migrate-to-astro/from-nextjs
timestamp: '2026-07-13T09:18:12.222139+00:00'
---

# Migrating from Next.js

Here are some key concepts and migration strategies to help you get started. Use the rest of our docs and our [Discord community](https://astro.build/chat) to keep going!

## Key Similarities between Next.js and Astro

[Section titled “Key Similarities between Next.js and Astro”](#key-similarities-between-nextjs-and-astro)

Next.js and Astro share some similarities that will help you migrate your project:

- The [syntax of](/en/reference/astro-syntax/#differences-between-astro-and-jsx). Writing Astro should feel familiar.`.astro`files is similar to JSX
- Astro projects can also be SSG or [SSR with page-level prerendering](/en/guides/on-demand-rendering/).
- Astro uses file-based routing, and [allows specially named pages to create dynamic routes](/en/guides/routing/#dynamic-routes).
- Astro is [component-based](/en/basics/astro-components/), and your markup structure will be similar before and after your migration.
- Astro has [official integrations for React, Preact, and Solid](/en/guides/integrations-guide/react/)so you can use your existing JSX components. Note that in Astro, these files**must**have a`.jsx`or`.tsx`extension.
- Astro has support for [installing NPM packages](/en/guides/imports/#npm-packages), including React libraries. Many of your existing dependencies will work in Astro.

## Key Differences between Next.js and Astro

[Section titled “Key Differences between Next.js and Astro”](#key-differences-between-nextjs-and-astro)

When you rebuild your Next.js site in Astro, you will notice some important differences:

- 
Next.js is a React single-page app, and uses `index.js`as your project’s root. Astro is a multi-page site, and`index.astro`is your home page.
- 
`.astro`components
- 
[content-driven](/en/concepts/why-astro/#content-driven): Astro was designed to showcase your content and to allow you to opt-in to interactivity only as needed. An existing Next.js app might be built for high client-side interactivity and may require advanced Astro techniques to include items that are more challenging to replicate using`.astro`components, such as dashboards.

## Convert your Next.js Project

[Section titled “Convert your Next.js Project”](#convert-your-nextjs-project)

Each project migration will look different, but there are some common actions you will perform when converting from Next.js to Astro.

### Create a new Astro project

[Section titled “Create a new Astro project”](#create-a-new-astro-project)

Use the `create astro` command for your package manager to launch Astro’s CLI wizard or choose a community theme from the [Astro Theme Showcase](https://astro.build/themes).

You can pass a `--template` argument to the `create astro` command to start a new Astro project with one of our official starters (e.g. `docs`, `blog`, `portfolio`). Or, you can [start a new project from any existing Astro repository on GitHub](/en/install-and-setup/#install-from-the-cli-wizard).

Then, copy your existing Next project files over to your new Astro project in a separate folder outside of `src`.

Visit [https://astro.new](https://astro.new) for the full list of official starter templates, and links for opening a new project in StackBlitz or CodeSandbox.

### Install integrations (optional)

[Section titled “Install integrations (optional)”](#install-integrations-optional)

You may find it useful to install some of [Astro’s optional integrations](/en/guides/integrations/) to use while converting your Next project to Astro:

- 
**@astrojs/react**: to reuse some existing React UI components in your new Astro site, or keep writing with React components.
- 
**@astrojs/mdx**: to bring existing MDX files from your Next project, or to use MDX in your new Astro site.

### Put your source code in `src`

[Section titled “Put your source code in src”](#put-your-source-code-in-src)

Following [Astro’s project structure](/en/basics/project-structure/):

- 
**Keep**Next’s`public/`folder untouched.Astro uses the `public/`directory for static assets, just like Next. There is no change needed to this folder, nor its contents.
- 
**Copy or Move**Next’s other files and folders (e.g.`pages`,`styles`etc.) into Astro’s`src/`folder as you rebuild your site, following[Astro’s project structure](/en/basics/project-structure/).Like Next, Astro’s `src/pages/`folder is a special folder used for file-based routing. All other folders are optional, and you can organize the contents of your`src/`folder any way you like. Other common folders in Astro projects include`src/layouts/`,`src/components`,`src/styles`,`src/scripts`.

### The Astro config file

[Section titled “The Astro config file”](#the-astro-config-file)

Astro has a configuration file at the root of your project called [ astro.config.mjs](/en/guides/configuring-astro/). This is used only for configuring your Astro project and any installed integrations, including 

[SSR adapters](/en/guides/deploy/).

### Tips: Convert JSX files to `.astro` files

[Section titled “Tips: Convert JSX files to .astro files”](#tips-convert-jsx-files-to-astro-files)

Here are some tips for converting a Next `.js` component into a `.astro` component:

- 
Use the returned JSX of the existing Next.js component function as the basis for your HTML template. 
- 
Change any [Next or JSX syntax to Astro](#reference-convert-nextjs-syntax-to-astro)or to HTML web standards. This includes`<Link>`,`<Script>`,`{children}`, and`className`, for example.
- 
Move any necessary JavaScript, including import statements, into a [“code fence” (](/en/basics/astro-components/#the-component-script). Note: JavaScript to`---`)[conditionally render content](/en/reference/astro-syntax/#dynamic-html)is often written inside the HTML template directly in Astro.
- 
Use `Astro.props`
- 
Decide whether any imported components also need to be converted to Astro. With the official integration installed, you can [use existing React components in your Astro file](/en/guides/framework-components/). But, you may want to convert them to`.astro`components, especially if they do not need to be interactive!
- 
Replace `getStaticProps()`with import statements or`import.meta.glob()``fetch()`to fetch external data.

See [an example of a Next  .js file converted step-by-step](#guided-example-next-data-fetching-to-astro).

#### Compare: JSX vs Astro

[Section titled “Compare: JSX vs Astro”](#compare-jsx-vs-astro)

Compare the following Next component and a corresponding Astro component:

### Migrating Layout Files

[Section titled “Migrating Layout Files”](#migrating-layout-files)

You may find it helpful to start by converting your Next.js layouts and templates into [Astro layout components](/en/basics/layouts/).

Next has two different methods for creating layout files, each of which handles layouts differently than Astro:

- 
The `pages`directory

Each Astro page explicitly requires `<html>`, `<head>`, and `<body>` tags to be present, so it is common to reuse a layout file across pages. Astro uses a [ <slot />](/en/basics/astro-components/#slots) for page content, with no import statement required. Note the standard HTML templating, and direct access to 

`<head>`:#### Migrating from Next.js’ `pages` directory

[Section titled “Migrating from Next.js’ pages directory”](#migrating-from-nextjs-pages-directory)

Your Next project may have a `pages/_document.jsx` file that imports React components to customize your app’s `<head>`:

- 
Make a new Astro layout file using only the returned JSX. 
- 
Replace any React components with `<html>`,`<head>`,`<slot>`, and other HTML standard tags.

#### Migrating from Next.js’ `/app` directory

[Section titled “Migrating from Next.js’ /app directory”](#migrating-from-nextjs-app-directory)

Next.js’ `app/` directory layout files are created with two files: a `layout.jsx` file to customize the `<html>` and `<body>` contents, and a `head.jsx` file to customize the `<head>` element contents.

- 
Make a new Astro layout file using only the returned JSX. 
- 
Replace both these files with a single Astro layout file that contains a page shell ( `<html>`,`<head>`, and`<body>`tags) and a`<slot/>`instead of React’s`{children}`prop:

### Migrating Pages and Posts

[Section titled “Migrating Pages and Posts”](#migrating-pages-and-posts)

In Next.js, your posts either live in `/pages` or `/app/routeName/page.jsx`.

In Astro, all your page content must live within `src/` unless you are using [content collections](/en/guides/content-collections/).

#### React pages

[Section titled “React pages”](#react-pages)

Your existing Next JSX (`.js`) pages will need to be [converted from JSX files to  .astro pages](#tips-convert-jsx-files-to-astro-files). You cannot use an existing JSX page file in Astro.

These [ .astro pages](/en/basics/astro-pages/) must be located within 

`src/pages/` and will have page routes generated automatically based on their file path.#### Markdown and MDX pages

[Section titled “Markdown and MDX pages”](#markdown-and-mdx-pages)

Astro has built-in support for Markdown and an optional integration for MDX files. You can reuse any existing [Markdown and MDX files](/en/guides/markdown-content/), but they may require some adjustments to their frontmatter, such as adding [Astro’s special  layout frontmatter property](/en/basics/layouts/#markdown-layouts). You will no longer need to manually create pages for each Markdown-generated route. These files can be placed within 

`src/pages/` to take advantage of automatic file-based routing.Alternatively, you can use [content collections](/en/guides/content-collections/) in Astro to store and manage your content. You will retrieve the content yourself and [generate those pages dynamically](/en/guides/content-collections/#generating-routes-from-content).

### Migrating Tests

[Section titled “Migrating Tests”](#migrating-tests)

As Astro outputs raw HTML, it is possible to write end-to-end tests using the output of the build step. Any end-to-end tests written previously might work out-of-the-box if you have been able to match the markup of your Next site. Testing libraries such as Jest and React Testing Library can be imported and used in Astro to test your React components.

See Astro’s [testing guide](/en/guides/testing/) for more.

## Reference: Convert Next.js Syntax to Astro

[Section titled “Reference: Convert Next.js Syntax to Astro”](#reference-convert-nextjs-syntax-to-astro)

### Next Links to Astro

[Section titled “Next Links to Astro”](#next-links-to-astro)

Convert any Next `<Link to="">`, `<NavLink>` etc. components to HTML `<a href="">` tags.

Astro does not use any special component for links, although you are welcome to build your own `<Link>` component. You can then import and use this `<Link>` just as you would any other component.

### Next Imports to Astro

[Section titled “Next Imports to Astro”](#next-imports-to-astro)

Update any [file imports](/en/guides/imports/) to reference relative file paths exactly. This can be done using [import aliases](/en/guides/typescript/#import-aliases), or by writing out a relative path in full.

Note that `.astro` and several other file types must be imported with their full file extension.

### Next Children Props to Astro

[Section titled “Next Children Props to Astro”](#next-children-props-to-astro)

Convert any instances of `{children}` to an Astro `<slot />`. Astro does not need to receive `{children}` as a function prop and will automatically render child content in a `<slot />`.

React components that pass multiple sets of children can be migrated to an Astro component using [named slots](/en/basics/astro-components/#named-slots).

See more about [specific  <slot /> usage in Astro](/en/basics/astro-components/#slots).

### Next Data Fetching to Astro

[Section titled “Next Data Fetching to Astro”](#next-data-fetching-to-astro)

Convert any instances of `getStaticProps()` to either `import.meta.glob()` or `getCollection()`/`getEntry()` in order to access data from other files in your project source. To [fetch remote data](/en/guides/data-fetching/), use `fetch()`.

These data requests are made in the frontmatter of the Astro component and use top-level await.

See more about local files imports with [ import.meta.glob()](/en/guides/imports/#importmetaglob), 

[querying with content collections](/en/guides/content-collections/#querying-build-time-collections)or

[fetching remote data](/en/guides/data-fetching/).

### Next Styling to Astro

[Section titled “Next Styling to Astro”](#next-styling-to-astro)

You may need to replace any [CSS-in-JS libraries](https://github.com/withastro/astro/issues/4432) (e.g. styled-components) with other available CSS options in Astro.

If necessary, convert any inline style objects (`style={{ fontWeight: "bold" }}`) to inline HTML style attributes (`style="font-weight:bold;"`). Or, use an [Astro  <style> tag](/en/guides/styling/#styling-in-astro) for scoped CSS styles.

Tailwind is supported after installing the [Tailwind Vite plugin](/en/guides/styling/#tailwind). No changes to your existing Tailwind code are required!

See more about [Styling in Astro](/en/guides/styling/).

### Next Image Plugin to Astro

[Section titled “Next Image Plugin to Astro”](#next-image-plugin-to-astro)

Convert any Next `<Image />` components to [Astro’s own image component](/en/guides/images/) in `.astro` or `.mdx` files, or to a [standard HTML  <img> / JSX <img />](/en/guides/images/#images-in-ui-framework-components) tag as appropriate in your React components.

Astro’s `<Image />` component works in `.astro` and `.mdx` files only. See a [full list of its component attributes](/en/reference/modules/astro-assets/#image-) and note that several will differ from Next’s attributes.

In React (`.jsx`) components, use standard JSX image syntax (`<img />`). Astro will not optimize these images, but you can install and use NPM packages for more flexibility.

You can learn more about [using images in Astro](/en/guides/images/) in the Images Guide.

## Guided example: Next data fetching to Astro

[Section titled “Guided example: Next data fetching to Astro”](#guided-example-next-data-fetching-to-astro)

Here is an example of Next.js Pokédex data fetch converted to Astro.

`pages/index.js` fetches and displays a list of the first 151 Pokémon using [the REST PokéAPI](https://pokeapi.co/).

Here’s how to recreate that in `src/pages/index.astro`, replacing `getStaticProps()` with `fetch()`.

- 
Identify the return() JSX. 
- 
Create `src/pages/index.astro`Use the return value of the Next function. Convert any Next or React syntax to Astro, including changing the case of any [HTML global attributes](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes).Note that: - 
`.map`just works!
- 
`className`becomes`class`.
- 
`<Link>`becomes`<a>`.
- 
The `<> </>`fragment is not required in Astro templating.
- 
`key`is a React attribute, and is not an attribute of`li`in Astro.
 
- 
- 
Add any needed imports, props, and JavaScript Note that: - the `getStaticProps`function is no longer needed. Data from the API is fetched directly in the code fence.
- A `<Layout>`component is imported and wraps the page templating.
 
- the 

## Community Resources

[Section titled “Community Resources”](#community-resources)

If you found (or made!) a helpful video or blog post about converting a Next.js site to Astro, [add it to this list](https://github.com/withastro/docs/edit/main/src/content/docs/en/guides/migrate-to-astro/from-nextjs.mdx)!

## More migration guides

[Contribute](/en/contribute/)

[Community](https://astro.build/chat)

[Sponsor](https://opencollective.com/astrodotbuild)

# Citations

1. Source page: https://docs.astro.build/en/guides/migrate-to-astro/from-nextjs
