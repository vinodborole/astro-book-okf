---
type: Web Page
title: Migrating from Gatsby | Docs
description: Tips for migrating an existing Gatsby project to Astro
resource: https://docs.astro.build/en/guides/migrate-to-astro/from-gatsby
timestamp: '2026-07-07T10:59:34.007706+00:00'
---

# Migrating from Gatsby

Here are some key concepts and migration strategies to help you get started. Use the rest of our docs and our Discord community to keep going!

## Key Similarities between Gatsby and Astro

Section titled “Key Similarities between Gatsby and Astro”Gatsby and Astro share some similarities that will help you migrate your project:

- 
The syntax of `.astro`files is similar to JSX. Writing Astro should feel familiar.
- 
Astro has built-in support for Markdown and an integration for using MDX files. Also, you can configure and continue to use many of your existing Markdown plugins. 
- 
Astro also has an official integration for using React components. Note that in Astro, React files **must**have a`.jsx`or`.tsx`extension.
- 
Astro has support for installing NPM packages, including React libraries. Many of your existing dependencies will work in Astro. 
- 
Like Gatsby, Astro projects can be SSG or SSR with page-level prerendering. 

## Key Differences between Gatsby and Astro

Section titled “Key Differences between Gatsby and Astro”When you rebuild your Gatsby site in Astro, you will notice some important differences:

- 
Gatsby projects are React single-page apps and use `index.js`as your project’s root. Astro projects are multi-page sites, and`index.astro`is your home page.
- 
Astro components are not written as exported functions that return page templating. Instead, you’ll split your code into a “code fence” for your JavaScript and a body exclusively for the HTML you generate. 
- 
Local file data: Gatsby uses GraphQL to retrieve data from your project files. Astro uses ESM imports and top-level await functions (e.g. `import.meta.glob()`,`getCollection()`) to import data from your project files. You can manually add GraphQL to your Astro project but it is not included by default.

## Convert your Gatsby Project

Section titled “Convert your Gatsby Project”Each project migration will look different, but there are some common actions you will perform when converting from Gatsby to Astro.

### Create a new Astro project

Section titled “Create a new Astro project”Use the `create astro` command for your package manager to launch Astro’s CLI wizard or choose a community theme from the Astro Theme Showcase.

You can pass a `--template` argument to the `create astro` command to start a new Astro project with one of our official starters (e.g. `docs`, `blog`, `portfolio`). Or, you can start a new project from any existing Astro repository on GitHub.

Then, copy your existing Gatsby project files over to your new Astro project into a separate folder outside of `src`.

Visit https://astro.new for the full list of official starter templates, and links for opening a new project in StackBlitz or CodeSandbox.

### Install integrations (optional)

Section titled “Install integrations (optional)”You may find it useful to install some of Astro’s optional integrations to use while converting your Gatsby project to Astro:

- 
**@astrojs/react**: to reuse some existing React UI components in your new Astro site or keep writing with React components.
- 
**@astrojs/mdx**: to bring existing MDX files from your Gatsby project, or to use MDX in your new Astro site.

### Put your code in `src`

Section titled “Put your code in src”Following Astro’s project structure:

- 
**Delete**Gatsby’s`public/`folder.Gatsby uses the `public/`directory for its build output, so you can safely discard this folder. You will no longer need a built version of your Gatsby site. (Astro uses`dist/`by default for the build output.)
- 
**Rename**Gatsby’s`static/`folder to`public/`, and use it as Astro’s`public/`folder.Astro uses a folder called `public/`for static assets. You can alternatively copy the contents of`static/`into your existing Astro`public/`folder.
- 
**Copy or Move**Gatsby’s other files and folders (e.g.`components`,`pages`, etc.) as needed into your Astro`src/`folder as you rebuild your site, following Astro’s project structure.Astro’s `src/pages/`folder is a special folder used for file-based routing to create your site’s pages and posts from`.astro`,`.md`and`.mdx`files. You will not have to configure any routing behavior for your Astro, Markdown, and MDX files.All other folders are optional, and you can organize the contents of your `src/`folder any way you like. Other common folders in Astro projects include`src/layouts/`,`src/components`,`src/styles`, and`src/scripts`.

### Tips: Convert JSX files to `.astro` files

Section titled “Tips: Convert JSX files to .astro files”Here are some tips for converting a Gatsby `.js` component into a `.astro` component:

- 
Use only the `return()`of the existing Gatsby component function as your HTML template.
- 
Change any Gatsby or JSX syntax to Astro syntax or to HTML web standards. This includes `<Link to="">`,`{children}`, and`className`, for example.
- 
Move any necessary JavaScript, including import statements, into a “code fence” ( `---`). Note: JavaScript to conditionally render content is often written inside the HTML template directly in Astro.
- 
Use `Astro.props`to access any additional props that were previously passed to your Gatsby function.
- 
Decide whether any imported components also need to be converted to Astro. With the official React integration installed, you can use existing React components in your Astro files. But, you may want to convert them to `.astro`components, especially if they do not need to be interactive!
- 
Remove any GraphQL queries. Instead, use import and `import.meta.glob()`statements to query your local files.

See an example from Gatsby’s Blog starter template converted step-by-step

#### Compare: `.jsx` vs `.astro`

Section titled “Compare: .jsx vs .astro”Compare the following Gatsby component and a corresponding Astro component:

### Migrating Layout Files

Section titled “Migrating Layout Files”You may find it helpful to start by converting your Gatsby layouts and templates into Astro layout components.

Each Astro page explicitly requires `<html>`, `<head>`, and `<body>` tags to be present, so it is common to reuse a layout file across pages. Astro uses a `<slot />` instead of React’s `{children}` prop for page content, with no import statement required. Your Gatsby `layout.js` and templates will not include these.

Note the standard HTML templating, and direct access to `<head>`:

You may also wish to reuse code from Gatsby’s `src/components/seo.js` to include additional site metadata. Notice that Astro uses neither `<Helmet>` nor `<Header>` but instead creates `<head>` directly. You may import and use components, even within `<head>`, to separate and organize your page content.

### Migrating Pages and Posts

Section titled “Migrating Pages and Posts”In Gatsby, your pages and posts may exist in `src/pages/` or outside of `src` in another folder, like `content`. In Astro, all your page content must live within `src/` unless you are using content collections.

#### React Pages

Section titled “React Pages”Your existing Gatsby JSX (`.js`) pages will need to be converted from JSX files to `.astro` pages. You cannot use an existing JSX page file in Astro.

These `.astro` pages must be located within `src/pages/` and will have page routes generated automatically based on their file path.

#### Markdown and MDX pages

Section titled “Markdown and MDX pages”Astro has built-in support for Markdown and an optional integration for MDX files. Your existing Markdown and MDX files can be reused but may require some adjustments to their frontmatter, such as adding Astro’s special `layout` frontmatter property. They can also be placed within `src/pages/` to take advantage of automatic file-based routing.

Alternatively, you can use content collections in Astro to store and manage your content. You will retrieve the content yourself and generate those pages dynamically.

### Migrating Tests

Section titled “Migrating Tests”As Astro outputs raw HTML, it is possible to write end-to-end tests using the output of the build step. Any end-to-end tests written previously might work out-of-the-box if you have been able to match the markup of the older Gatsby site. Testing libraries such as Jest and React Testing Library can be imported and used in Astro to test your React components.

See Astro’s testing guide for more.

### Repurpose config files

Section titled “Repurpose config files”Gatsby has several top-level configuration files that also include site and page metadata and are used for routing. You will not use any of these `gatsby-*.js` files in your Astro project, but there may be some content that you can reuse as you build your Astro project:

- 
`gatsby-config.js`: Move your`siteMetadata: {}`into`src/data/siteMetadata.js`(or`siteMetadata.json`) to import data about your site (title, description, social accounts, etc.) into page layouts.
- 
`gatsby-browser.js`: Consider adding anything used here directly into your main layout’s`<head>`tag.
- 
`gatsby-node.js`: You will not need to create your own nodes in Astro, but viewing the schema in this file may help you with defining types in your Astro project.
- 
`gatsby-ssr.js`: If you choose to use SSR in Astro, you will add and configure the SSR adapter of your choice directly in`astro.config.mjs`.

## Reference: Convert to Astro Syntax

Section titled “Reference: Convert to Astro Syntax”The following are some examples of Gatsby-specific syntax that you will need to convert to Astro. See more differences between Astro and JSX in the guide to writing Astro components.

### Gatsby Links to Astro

Section titled “Gatsby Links to Astro”Convert any Gatsby `<Link to="">`, `<NavLink>` etc. components to HTML `<a href="">` tags.

Astro does not use any special component for links, although you are welcome to build your own `<Link>` component. You can then import and use this `<Link>` just as you would any other component.

### Gatsby Imports to Astro

Section titled “Gatsby Imports to Astro”If necessary, update any file imports to reference relative file paths exactly. This can be done using import aliases, or by writing out a relative path in full.

Note that `.astro` and several other file types must be imported with their full file extension.

### Gatsby Children Props to Astro

Section titled “Gatsby Children Props to Astro”Convert any instances of `{children}` to an Astro `<slot />`. Astro does not need to receive `{children}` as a function prop and will automatically render child content in a `<slot />`.

React components that pass multiple sets of children can be migrated to an Astro component using named slots.

See more about specific `<slot />` usage in Astro.

### Gatsby Styling to Astro

Section titled “Gatsby Styling to Astro”You may need to replace any CSS-in-JS libraries (e.g. styled-components) with other available CSS options in Astro.

If necessary, convert any inline style objects (`style={{ fontWeight: "bold" }}`) to inline HTML style attributes (`style="font-weight:bold;"`). Or, use an Astro `<style>` tag for scoped CSS styles.

Tailwind is supported after installing the Tailwind Vite plugin. No changes to your existing Tailwind code are required!

Global styling is achieved in Gatsby using CSS imports in `gatsby-browser.js`. In Astro, you will import `.css` files directly into a main layout component to achieve global styles.

See more about Styling in Astro.

### Gatsby Image Plugin to Astro

Section titled “Gatsby Image Plugin to Astro”Convert Gatsby’s `<StaticImage />` and `<GatsbyImage />` components to Astro’s own image integration components, or to a standard HTML `<img>` / JSX `<img />` tag as appropriate in your React components.

Astro’s `<Image />` component works in `.astro` and `.mdx` files only. See a full list of its component attributes and note that several will differ from Gatsby’s attributes.

To continue using images in Markdown (`.md`) files using standard Markdown syntax (`![]()`), you may need to update the link. Using the HTML `<img>` tag directly is not supported in `.md` files for local images, and must be converted to Markdown syntax.

In React (`.jsx`) components, use standard JSX image syntax (`<img />`). Astro will not optimize these images, but you can install and use NPM packages for more flexibility.

You can learn more about using images in Astro in the Images Guide.

### Gatsby GraphQL to Astro

Section titled “Gatsby GraphQL to Astro”Remove all references to GraphQL queries, and instead use `import.meta.glob()` to access data from your local files.

Or, if using content collections, query your Markdown and MDX files using `getEntry()` and `getCollection()`.

These data requests are made in the frontmatter of the Astro component using the data.

## Guided example: Gatsby layout to Astro

Section titled “Guided example: Gatsby layout to Astro”This example converts the main project layout (`layout.js`) from Gatsby’s blog starter to `src/layouts/Layout.astro`.

This page layout shows one header when visiting the home page, and a different header with a link back to Home for all other pages.

- 
Identify the `return()`JSX.
- 
Create `Layout.astro`and add this`return`value, converted to Astro syntax.Note that: - `{new Date().getFullYear()}`just works 🎉
- `{children}`becomes- `<slot />`🦥
- `className`becomes- `class`📛
- `Gatsby`becomes- `Astro`🚀
 
- 
Add a page shell so that your layout provides each page with the necessary parts of an HTML document: 
- 
Add any needed imports, props, and JavaScript To conditionally render a header based on the page route and title in Astro: - Provide the props via `Astro.props`. (Remember: your Astro templating accesses props from its frontmatter, not passed into a function.)
- Use a ternary operator to show one heading if this is the home page, and a different heading otherwise.
- Remove variables for `{header}`and`{isRootPath}`as they are no longer needed.
- Replace Gatsby’s `<Link/>`tags with`<a>`anchor tags.
- Use `class`instead of`className`.
- Import a local stylesheet from your project for the class names to take effect.
 
- Provide the props via 
- 
Update `index.astro`to use this new layout and pass it the necessary`title`and`pathname`props:
- 
To test the conditional header, create a second page, `about.astro`using the same pattern:You should see a link to “Home” only when visiting the About page. 

## Community Resources

Section titled “Community Resources”If you found (or made!) a helpful video or blog post about converting a Gatsby site to Astro, add it to this list!

# Citations

1. Source page: https://docs.astro.build/en/guides/migrate-to-astro/from-gatsby
