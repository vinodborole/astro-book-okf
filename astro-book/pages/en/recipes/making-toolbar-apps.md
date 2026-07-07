---
type: Web Page
title: Create a dev toolbar app | Docs
description: Learn how to create a dev toolbar app for your site.
resource: https://docs.astro.build/en/recipes/making-toolbar-apps
timestamp: '2026-07-07T10:59:34.007706+00:00'
---

# Create a dev toolbar app

Astro includes a development toolbar that you can use to inspect your site, check for accessibility and performance issues, and more. This toolbar can be extended with custom apps.

## Build a motivational dev toolbar app

Section titled “Build a motivational dev toolbar app”In this recipe, you’ll learn how to create a dev toolbar app that helps you stay motivated while working on your site. This app will display a motivational message every time you toggle it on.

### Creating the Astro integration

Section titled “Creating the Astro integration”Dev toolbar apps can only be added by Astro Integrations using the `astro:config:setup` hook. You will need to create both a toolbar app and the integration that will add it to the toolbar of your existing Astro project.

- 
In the root of your existing Astro project, create a new folder named `my-toolbar-app/`for your app and integration files. Create two new files in this folder:`app.ts`and`my-integration.ts`.- ## Directory- **my-toolbar-app/**- **app.ts**
- **my-integration.ts**
 
- ## Directorysrc/- ## Directorypages/- …
 
- …
 
- astro.config.mjs
- package.json
- tsconfig.json
 
- 
In `my-integration.ts`, add the following code to provide both the name of your integration and the`addDevToolbarApp()`function needed to add your dev toolbar app with the`astro:config:setup`hook:The `entrypoint`is the path to your dev toolbar app file**relative to the root of your existing Astro project**, not to the integration folder (`my-toolbar-app`) itself.To use relative paths for entrypoints, get the path to the current file using `import.meta.url`and resolve the path to the entrypoint from there.
- 
To use this integration in your project, add it to the `integrations`array in your`astro.config.mjs`file.
- 
If not already running, start the dev server. If your integration has been successfully added to your project, you should see a new “undefined” app in the dev toolbar. But, you will also see an error message that your dev toolbar app has failed to load. This is because you have not yet built the app itself. You will do that in the next section. 

### Creating the app

Section titled “Creating the app”Dev toolbar apps are defined using the `defineToolbarApp()` function from the `astro/toolbar` module. This function takes an object with an `init()` function that will be called when the dev toolbar app is loaded.

This `init()` function contains your app logic to render elements to the screen, send and receive client-side events from the dev toolbar, and communicate with the server.

To display motivational messages on the screen, you will use the `canvas` property to access a standard ShadowRoot. Elements can be created and added to the ShadowRoot using the standard DOM APIs.

- 
Copy the following code into `my-toolbar-app/app.ts`. This provides a list of motivational messages, and the logic to create a new`<h1>`element with a random message:
- 
Start the dev server if it is not already running and toggle the app on in the dev toolbar. If your app is working successfully, you will see a motivational message displayed in the top-left corner of the screen. (And, it’s true!) However, this message will not change when the app is toggled on and off, as the `init()`function is only called once when the app is loaded.
- 
To add client-side interactivity to your app, add the `app`argument and use`onAppToggled()`to select a new random message each time your toolbar app is toggled on:
- 
In your browser preview, toggle your app on and off several times. With this change, a new random message will be selected every time you toggle the app on, providing you with an infinite source of motivation! 

## Building apps with a UI framework

Section titled “Building apps with a UI framework”UI frameworks like React, Vue, or Svelte can also be used to create dev toolbar apps. These frameworks provide a more declarative way to create UIs and can make your code more maintainable and easier to read.

The same motivational dev toolbar app built into your existing Astro project earlier on this page with JavaScript can be built using a UI framework (e.g. Preact) instead. Depending on your chosen framework, you may or may not require a build step.

However you choose to build your dev toolbar app, using JavaScript or a UI framework, you will still need to create the integration that adds your app to the dev toolbar.

### Without a build step

Section titled “Without a build step”If your framework supports it, you can create a dev toolbar app without a build step. For example, you can use Preact’s `h` function to create elements and render them directly to the ShadowRoot:

Alternatively, the `htm` package is a good choice for creating dev toolbar apps without a build step, offering native integration for React and Preact and support for other frameworks:

In both cases, you can now start your project and see the motivational message displayed in the top-left corner of the screen when you toggle the app on.

### With a build step

Section titled “With a build step”Astro does not preprocess JSX code in dev toolbar apps, so a build step is required in order to use JSX components in your dev toolbar app.

The following steps will use TypeScript to do this, but any other tools that compile JSX code will also work (e.g. Babel, Rollup, ESBuild).

- 
Install TypeScript inside your project: 
- 
Create a `tsconfig.json`file in the root of your toolbar app’s folder with the appropriate settings to build and for the framework you’re using (React, Preact, Solid). For example, for Preact:
- 
Adjust the `entrypoint`in your integration to point to the compiled file, remembering that this file is relative to the root of your Astro project:
- 
Run `tsc`to build your toolbar app, or`tsc --watch`to automatically rebuild your app when you make changes.With these changes, you can now rename your `app.ts`file to`app.tsx`(or`.jsx`) and use JSX syntax to create your dev toolbar app:

You should now have all the tools you need to create a dev toolbar app using a UI framework of your choice!

Recipes

# Citations

1. Source page: https://docs.astro.build/en/recipes/making-toolbar-apps
