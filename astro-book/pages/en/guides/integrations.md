---
type: Web Page
title: Working with integrations | Docs
description: Learn how to add, configure, and build integrations for your Astro project.
resource: https://docs.astro.build/en/guides/integrations
timestamp: '2026-07-07T10:59:34.007706+00:00'
---

# Working with integrations

**Astro integrations** add new functionality and behaviors for your project with only a few lines of code. You can use an official integration, integrations built by the community or even build a custom integration yourself.

Integrations can…

- Unlock React, Vue, Svelte, Solid, and other popular UI frameworks with a renderer.
- Enable on-demand rendering with an SSR adapter.
- Integrate tools like MDX, and Partytown with a few lines of code.
- Add new features to your project, like automatic sitemap generation.
- Write custom code that hooks into the build process, dev server, and more.

Browse or search the complete set of hundreds of official and community integrations in our integrations directory. Find packages to add to your Astro project for authentication, analytics, performance, SEO, accessibility, UI, developer tools, and more.

## Official integrations

Section titled “Official integrations”The following integrations are maintained by Astro.

### Front-end frameworks

### Adapters

### Other integrations

## Automatic integration setup

Section titled “Automatic integration setup”Astro includes an `astro add` command to automate the setup of official integrations. Several community plugins can also be added using this command. Please check each integration’s own documentation to see whether `astro add` is supported, or whether you must install manually.

Run the `astro add` command using the package manager of your choice and our automatic integration wizard will update your configuration file and install any necessary dependencies.

It’s even possible to add multiple integrations at the same time!

If you see any warnings like `Cannot find package '[package-name]'` after adding an integration, your package manager may not have installed peer dependencies for you. To install these missing packages, run the following command:

### Manual installation

Section titled “Manual installation”Astro integrations are always added through the `integrations` property in your `astro.config.mjs` file.

There are three common ways to import an integration into your Astro project:

- 
Import your own integration from a local file inside your project. 
- 
Write your integration inline, directly in your config file. 

Check out the Integration API reference to learn all of the different ways that you can write an integration.

#### Installing an npm package

Section titled “Installing an npm package”Install an npm package integration using a package manager, and then update `astro.config.mjs` manually.

For example, to install the `@astrojs/sitemap` integration:

- 
Install the integration to your project dependencies using your preferred package manager: 
- 
Import the integration to your `astro.config.mjs`file, and add it to your`integrations[]`array, along with any configuration options:Note that different integrations may have different configuration settings. Read each integration’s documentation, and apply any necessary config options to your chosen integration in `astro.config.mjs`.

### Custom options

Section titled “Custom options”Integrations are almost always authored as factory functions that return the actual integration object. This lets you pass arguments and options to the factory function that customize the integration for your project.

### Toggle an integration

Section titled “Toggle an integration”Falsy integrations are ignored, so you can toggle integrations on & off without worrying about left-behind `undefined` and boolean values.

## Upgrading integrations

Section titled “Upgrading integrations”To upgrade all official integrations at once, run the `@astrojs/upgrade` command. This will upgrade both Astro and all official integrations to their latest versions.

### Automatic upgrading

Section titled “Automatic upgrading”### Manual upgrading

Section titled “Manual upgrading”To upgrade one or more integrations manually, use the appropriate command for your package manager.

## Removing an integration

Section titled “Removing an integration”- 
To remove an integration, first uninstall the integration from your project. 
- 
Next, remove the integration from your `astro.config.*`file:

## Finding more integrations

Section titled “Finding more integrations”You can find many integrations developed by the community in the Astro Integrations Directory. Follow links there for detailed usage and configuration instructions.

## Building your own integration

Section titled “Building your own integration”Astro’s Integration API is inspired by Rollup and Vite, and designed to feel familiar to anyone who has ever written a Rollup or Vite plugin before.

Check out the Integration API reference to learn what integrations can do and how to write one yourself.

## Publishing your integration to npm

Section titled “Publishing your integration to npm”Publishing an Astro component is a great way to reuse your existing work across your projects, and to share with the wider Astro community at large. Astro components can be published directly to and installed from npm, just like any other JavaScript package.

Looking for inspiration? Check out some of our favorite themes and components from the Astro community. You can also search npm to see the entire public catalog.

Check out Astro community’s component template for a community-supported, out-of-the-box template!

### Quick start

Section titled “Quick start”To get started developing your component quickly, you can use a template already set up for you.

### Creating a package

Section titled “Creating a package”Before diving in, it will help to have a basic understanding of:

To create a new package, configure your development environment to use **workspaces** within your project. This will allow you to develop your component alongside a working copy of Astro.

- ## Directorymy-new-component-directory/- ## Directorydemo/- … for testing and demonstration
 
- package.json
- ## Directorypackages/- ## Directorymy-component/- index.js
- package.json
- … additional files used by the package
 
 
 

This example, named `my-project`, creates a project with a single package, named `my-component`, and a `demo/` directory for testing and demonstrating the component.

This is configured in the project root’s `package.json` file:

In this example, multiple packages can be developed together from the `packages` directory. These packages can also be referenced from `demo`, where you can install a working copy of Astro.

There are two initial files that will make up your individual package: `package.json` and `index.js`.

`package.json`

Section titled “package.json”The `package.json` in the package directory includes all of the information related to your package, including its description, dependencies, and any other package metadata.

`description`

Section titled “description”A short description of your component used to help others know what it does.

The module format used by Node.js and Astro to interpret your `index.js` files.

Use `"type": "module"` so that your `index.js` can be used as an entrypoint with `import` and `export` .

`homepage`

Section titled “homepage”The url to the project homepage.

This is a great way to direct users to an online demo, documentation, or homepage for your project.

`exports`

Section titled “exports”The entry points of a package when imported by name.

In this example, importing `my-component` would use `index.js`, while importing `my-component/astro` or `my-component/react` would use `MyAstroComponent.astro` or `MyReactComponent.jsx` respectively.

An optional optimization to exclude unnecessary files from the bundle shipped to users via npm. Note that **only files listed here will be included in your package**, so if you add or change files necessary for your package to work, you must update this list accordingly.

`keywords`

Section titled “keywords”An array of keywords relevant to your component, used to help others find your component on npm and in any other search catalogs.

Add `astro-component`, `astro-integration`, or `withastro` as a special keyword to maximize its discoverability in the Astro ecosystem.

Keywords are also used by our integrations library! See below for a full list of keywords we look for in npm.

`index.js`

Section titled “index.js”The main **package entrypoint** used whenever your package is imported.

This allows you to package multiple components together into a single interface.

##### Example: Using named imports

Section titled “Example: Using named imports”##### Example: Using namespace imports

Section titled “Example: Using namespace imports”##### Example: Using individual imports

Section titled “Example: Using individual imports”### Developing your package

Section titled “Developing your package”Astro does not have a dedicated “package mode” for development. Instead, you should use a demo project to develop and test your package inside of your project. This can be a private website only used for development, or a public demo/documentation website for your package.

If you are extracting components from an existing project, you can even continue to use that project to develop your now-extracted components.

### Testing your component

Section titled “Testing your component”Astro does not currently ship a test runner. *(If you are interested in helping out with this, join us on Discord!)*

In the meantime, our current recommendation for testing is:

- 
Add a test `fixtures`directory to your`demo/src/pages`directory.
- 
Add a new page for every test that you’d like to run. 
- 
Each page should include some different component usage that you’d like to test. 
- 
Run `astro build`to build your fixtures, then compare the output of the`dist/__fixtures__/`directory to what you expected.- ## Directorymy-project/demo/src/pages/__fixtures__/- test-name-01.astro
- test-name-02.astro
- test-name-03.astro
 
 

### Publishing your component

Section titled “Publishing your component”Once you have your package ready, you can publish it to npm using the `npm publish` command. If that fails, make sure that you have logged in via `npm login` and that your `package.json` is correct. If it succeeds, you’re done!

Notice that there was no `build` step for Astro packages. Any file type that Astro supports natively, such as `.astro`, `.ts`, `.jsx`, and `.css`, can be published directly without a build step.

If you need another file type that isn’t natively supported by Astro, add a build step to your package. This advanced exercise is left up to you.

### Integrations library

Section titled “Integrations library”Share your hard work by adding your integration to our integrations library!

Do you need some help building your integration, or just want to meet other integrations builders? We have a dedicated `#integrations` channel on our Discord server. Come say hi!

`package.json` data

Section titled “package.json data”The library is automatically updated weekly, pulling in every package published to npm with the `astro-component`, `astro-integration`, or `withastro` keyword.

The integrations library reads the `name`, `description`, `repository`, and `homepage` data from your `package.json`.

Avatars are a great way to highlight your brand in the library! Once your package is published you can file a GitHub issue with your avatar attached and we will add it to your listing.

Need to override the information our library reads from npm? No problem! File an issue with the updated information and we’ll make sure the custom `name`, `description`, or `homepage` is used instead.

#### Categories

Section titled “Categories”In addition to the required `astro-component`, `astro-integration`, or `withastro` keyword, special keywords are also used to automatically organize packages. Including any of the keywords below will add your integration to the matching category in our integrations library.

| category | keywords | 
|---|---|
| Accessibility | `a11y`,`accessibility` | 
| Adapters | `astro-adapter` | 
| Analytics | `analytics` | 
| CSS + UI | `css`,`ui`,`icon`,`icons`,`renderer` | 
| Frameworks | `renderer` | 
| Content Loaders | `astro-loader` | 
| Images + Media | `media`,`image`,`images`,`video`,`audio` | 
| Performance + SEO | `performance`,`perf`,`seo`,`optimization` | 
| Dev Toolbar | `devtools`,`dev-overlay`,`dev-toolbar` | 
| Utilities | `tooling`,`utils`,`utility` | 

Packages that don’t include any keyword matching a category will be shown as `Uncategorized`.

We encourage you to share your work, and we really do love seeing what our talented Astronauts create. Come and share what you create with us in our Discord or mention @astrodotbuild in a Tweet!

Learn

# Citations

1. Source page: https://docs.astro.build/en/guides/integrations
