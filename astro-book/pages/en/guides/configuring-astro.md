---
type: Web Page
title: Configuration overview | Docs
description: Get to know the ways you can configure and customize your new project
  and your development experience.
resource: https://docs.astro.build/en/guides/configuring-astro
timestamp: '2026-07-07T10:59:34.007706+00:00'
---

# Configuration overview

Astro is a flexible, unopinionated framework that allows you to configure your project in many different ways. This means that getting started with a new project might feel overwhelming: there is no “one best way” to set up your Astro project!

The guides in this “Configuration” section will help you familiarize yourself with the various files that allow you to configure and customize aspects of your project and development environment.

If this is your first Astro project, or if it’s been a while since you’ve set up a new project, use the following guides and reference in the documentation for assistance.

## The Astro config File

Section titled “The Astro config File”The Astro config file is a JavaScript file included at the root of every starter project:

It is only required if you have something to configure, but most projects will use this file. The `defineConfig()` helper provides automatic IntelliSense in your IDE and is where you will add all your configuration options to tell Astro how to build and render your project to HTML.

We recommend using the default file format `.mjs` in most cases, or `.ts` if you want to write TypeScript in your config file. However, `astro.config.js` is also supported.

## The TypeScript config File

Section titled “The TypeScript config File”Every Astro starter project includes a `tsconfig.json` file in your project. Astro’s component script is TypeScript, which provides Astro’s editor tooling and allows you to optionally add syntax to your JavaScript for type checking of your own project code.

Use the `tsconfig.json` file to configure the TypeScript template that will perform type checks on your code, configure TypeScript plugins, set import aliases, and more.

## Development Experience

Section titled “Development Experience”While you work in development mode, you can take advantage of your code editor and other tools to improve the Astro developer experience.

Astro provides its own official VS Code extension and is compatible with several other popular editor tools. Astro also provides a customizable toolbar that displays in your browser preview while the dev server is running. You can install and even build your own toolbar apps for additional functionality.

## Common new project tasks

Section titled “Common new project tasks”Here are some first steps you might choose to take with a new Astro project.

### Add your deployment domain

Section titled “Add your deployment domain”For generating your sitemap and creating canonical URLs, configure your deployment URL in the `site` option. If you are deploying to a path (e.g. `www.example.com/docs`), you can also configure a `base` for the root of your project.

Additionally, different deployment hosts may have different behavior regarding trailing slashes at the end of your URLs. (e.g. `example.com/about` vs `example.com/about/`). Once your site is deployed, you may need to configure your `trailingSlash` preference.

### Add site metadata

Section titled “Add site metadata”Astro does not use its configuration file for common SEO or meta data, only for information required to build your project code and render it to HTML.

Instead, this information is added to your page `<head>` using standard HTML `<link>` and `<meta>` tags, just as if you were writing plain HTML pages.

One common pattern for Astro sites is to create a `<Head />` `.astro` component that can be added to a common layout component so it can apply to all your pages.

Because `Head.astro` is just a regular Astro component, you can import files and receive props passed from other components, such as a specific page title.

# Citations

1. Source page: https://docs.astro.build/en/guides/configuring-astro
