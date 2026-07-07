---
type: Web Page
title: Migrating from Create React App (CRA) | Docs
description: Tips for migrating an existing Create React App project to Astro
resource: https://docs.astro.build/en/guides/migrate-to-astro/from-create-react-app
timestamp: '2026-07-07T10:59:34.007706+00:00'
---

# Migrating from Create React App (CRA)

Astro’s React integration provides support for using React components inside Astro components, including entire React apps like Create React App (CRA)!

Many apps will “just work” as full React apps when you add them directly to your Astro project with the React integration installed. This is a great way to get your project up and running immediately and keep your app functional while you migrate to Astro.

Over time, you can convert your structure piece-by-piece to a combination of `.astro` and `.jsx` components. You will probably discover you need fewer React components than you think!

Here are some key concepts and migration strategies to help you get started. Use the rest of our docs and our Discord community to keep going!

## Key Similarities between CRA and Astro

Section titled “Key Similarities between CRA and Astro”- 
The syntax of `.astro`files is similar to JSX. Writing Astro should feel familiar.
- 
Astro uses file-based routing, and allows specially named pages to create dynamic routes. 
- 
Astro is component-based, and your markup structure will be similar before and after your migration. 
- 
Astro has official integrations for React, Preact, and Solid so you can use your existing JSX components. Note that in Astro, these files **must**have a`.jsx`or`.tsx`extension.
- 
Astro has support for installing NPM packages, including React libraries. Many of your existing dependencies will work in Astro. 

## Key Differences between CRA and Astro

Section titled “Key Differences between CRA and Astro”When you rebuild your CRA site in Astro, you will notice some important differences:

- 
CRA is a single-page application that uses `index.js`as your project’s root. Astro is a multi-page site, and`index.astro`is your home page.
- 
`.astro`components are not written as exported functions that return page templating. Instead, you’ll split your code into a “code fence” for your JavaScript and a body exclusively for the HTML you generate.
- 
content-driven: Astro was designed to showcase your content and to allow you to opt-in to interactivity only as needed. An existing CRA app might be built for high client-side interactivity and may require advanced Astro techniques to include items that are more challenging to replicate using `.astro`components, such as dashboards.

## Add your CRA to Astro

Section titled “Add your CRA to Astro”Your existing app can be rendered directly inside a new Astro project, often with no changes to your app’s code.

### Create a new Astro project

Section titled “Create a new Astro project”Use the `create astro` command for your package manager to launch Astro’s CLI wizard and select a new “empty” Astro project.

### Add integrations and dependencies

Section titled “Add integrations and dependencies”Add the React integration using the `astro add` command for your package manager. If your app uses other packages supported by the `astro add` command, like Tailwind and MDX, you can add them all with one command:

If your CRA requires any dependencies (e.g. NPM packages), then install them individually using the command line or by adding them to your new Astro project’s `package.json` manually and then running an install command. Note that many, but not all, React dependencies will work in Astro.

### Add your existing app files

Section titled “Add your existing app files”Copy your existing Create React App (CRA) project source files and folders (e.g. `components`, `hooks`, `styles`, etc.) into a new folder inside `src/`, keeping its file structure so your app will continue to work. Note that all `.js` file extensions must be renamed to `.jsx` or `.tsx`.

Do not include any configuration files. You will use Astro’s own `astro.config.mjs`, `package.json`, and `tsconfig.json`.

Move the contents of your app’s `public/` folder (e.g. static assets) into Astro’s `public/` folder.

- ## Directorypublic/- logo.png
- favicon.ico
- …
 
- ## Directorysrc/- ## Directorycra-project/- App.jsx
- …
 
- ## Directorypages/- index.astro
 
 
- astro.config.mjs
- package.json
- tsconfig.json

### Render your app

Section titled “Render your app”Import your app’s root component in the frontmatter section of `index.astro`, then render the `<App />` component in your page template:

Your app needs a client directive for interactivity. Astro will render your React app as static HTML until you opt-in to client-side JavaScript.

Use `client:load` to ensure your app loads immediately from the server, or `client:only="react"` to skip rendering on the server and run your app entirely client-side.

## Convert your CRA to Astro

Section titled “Convert your CRA to Astro”After adding your existing app to Astro, you will probably want to convert your app itself to Astro!

You will replicate a similar component-based design using Astro HTML templating components for your basic structure while importing and including individual React components (which may themselves be entire apps!) for islands of interactivity.

Every migration will look different and can be done incrementally without disrupting your working app. Convert individual pieces at your own pace so that more and more of your app is powered by Astro components over time.

As you convert your React app, you will decide which React components you will rewrite as Astro components. Your only restriction is that Astro components can import React components, but React components must only import other React components:

Instead of importing Astro components into React components, you can nest React components inside a single Astro component:

You may find it helpful to learn about Astro islands and Astro components before restructuring your CRA as an Astro project.

### Compare: JSX vs Astro

Section titled “Compare: JSX vs Astro”Compare the following CRA component and a corresponding Astro component:

### Converting JSX files to `.astro` files

Section titled “Converting JSX files to .astro files”Here are some tips for converting a CRA `.js` component into a `.astro` component:

- 
Use the returned JSX of the existing CRA component function as the basis for your HTML template. 
- 
Change any CRA or JSX syntax to Astro or to HTML web standards. This includes `{children}`and`className`, for example.
- 
Move any necessary JavaScript, including import statements, into a “code fence” ( `---`). Note: JavaScript to conditionally render content is often written inside the HTML template directly in Astro.
- 
Use `Astro.props`to access any additional props that were previously passed to your CRA function.
- 
Decide whether any imported components also need to be converted to Astro. You can keep them as React components for now, or forever. But, you may eventually want to convert them to `.astro`components, especially if they do not need to be interactive!
- 
Replace `useEffect()`with import statements or`import.meta.glob()`to query your local files. Use`fetch()`to fetch external data.

### Migrating Tests

Section titled “Migrating Tests”As Astro outputs raw HTML, it is possible to write end-to-end tests using the output of the build step. Any end-to-end tests written previously might work out-of-the-box if you have been able to match the markup of your CRA site. Testing libraries such as Jest and React Testing Library can be imported and used in Astro to test your React components.

See Astro’s testing guide for more.

## Reference: Convert CRA Syntax to Astro

Section titled “Reference: Convert CRA Syntax to Astro”### CRA Imports to Astro

Section titled “CRA Imports to Astro”Update any file imports to reference relative file paths exactly. This can be done using import aliases, or by writing out a relative path in full.

Note that `.astro` and several other file types must be imported with their full file extension.

### CRA Children Props to Astro

Section titled “CRA Children Props to Astro”Convert any instances of `{children}` to an Astro `<slot />`. Astro does not need to receive `{children}` as a function prop and will automatically render child content in a `<slot />`.

React components that pass multiple sets of children can be migrated to an Astro component using named slots.

See more about specific `<slot />` usage in Astro.

### CRA Data Fetching to Astro

Section titled “CRA Data Fetching to Astro”Fetching data in a Create React App component is similar to Astro, with some slight differences.

You will need to remove any instances of a side effect hook (`useEffect`) for either `import.meta.glob()` or `getCollection()`/`getEntry()` to access data from other files in your project source.

To fetch remote data, use `fetch()`.

These data requests are made in the frontmatter of the Astro component and use top-level await.

See more about local files imports with `import.meta.glob()`, querying with content collections or fetching remote data.

### CRA Styling to Astro

Section titled “CRA Styling to Astro”You may need to replace any CSS-in-JS libraries (e.g. styled-components) with other available CSS options in Astro.

If necessary, convert any inline style objects (`style={{ fontWeight: "bold" }}`) to inline HTML style attributes (`style="font-weight:bold;"`). Or, use an Astro `<style>` tag for scoped CSS styles.

Tailwind is supported after installing the Tailwind Vite plugin. No changes to your existing Tailwind code are required!

See more about Styling in Astro.

## Troubleshooting

Section titled “Troubleshooting”Your CRA might “just work” in Astro! But, you may likely need to make minor adjustments to duplicate your existing app’s functionality and/or styles.

If you cannot find your answers within these docs, please visit the Astro Discord and ask questions in our support forum!

## Community Resources

Section titled “Community Resources”If you found (or made!) a helpful video or blog post about converting a Create React App to Astro, add it to this list!

# Citations

1. Source page: https://docs.astro.build/en/guides/migrate-to-astro/from-create-react-app
