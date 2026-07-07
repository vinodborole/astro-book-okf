---
type: Web Page
title: Install Astro | Docs
description: How to install Astro and start a new project.
resource: https://docs.astro.build/en/install-and-setup
timestamp: '2026-07-07T10:59:34.007706+00:00'
---

# Install Astro

The `create astro` CLI command is the fastest way to start a new Astro project from scratch. It will walk you through every step of setting up your new Astro project and allow you to choose from a few different official starter templates.

You can also run the CLI command with the `template` flag to begin your project using any existing theme or starter template. Explore our themes and starters showcase where you can browse themes for blogs, portfolios, documentation sites, landing pages, and more!

To install Astro manually instead, see our step-by-step manual installation guide.

Prefer to try Astro in your browser? Visit astro.new to browse our starter templates and spin up a new Astro project without ever leaving your browser.

## Prerequisites

Section titled “Prerequisites”- **Node.js**-- `v22.12.0`or higher. Odd-numbered versions like- `v23`are not supported.
- **Text editor**- We recommend VS Code with our Official Astro extension.
- **Terminal**- Astro is accessed through its command-line interface (CLI).

## Browser compatibility

Section titled “Browser compatibility”Astro is built with Vite which targets browsers with modern JavaScript support by default. For a complete reference, you can see the list of currently supported browser versions in Vite.

## Install from the CLI wizard

Section titled “Install from the CLI wizard”You can run `create astro` anywhere on your machine, so there’s no need to create a new empty directory for your project before you begin. If you don’t have an empty directory yet for your new project, the wizard will help create one for you automatically.

- 
Run the following command in your terminal to start the install wizard: If all goes well, you will see a success message followed by some recommended next steps. 
- 
Now that your project has been created, you can `cd`into your new project directory to begin using Astro.
- 
If you skipped the “Install dependencies?” step during the CLI wizard, then be sure to install your dependencies before continuing. 
- 
You can now start the Astro dev server and see a live preview of your project while you build! 

## CLI installation flags

Section titled “CLI installation flags”You can run the `create astro` command with additional flags to customize the setup process (e.g. answering “yes” to all questions, skipping the Houston animation) or your new project (e.g. install git or not, add integrations).

### Add integrations

Section titled “Add integrations”You can start a new Astro project and install any official integrations or community integrations that support the `astro add` command at the same time by passing the `--add` argument to the `create astro` command.

Run the following command in your terminal, substituting any integration that supports the `astro add` command:

### Use a theme or starter template

Section titled “Use a theme or starter template”You can start a new Astro project based on an official example or the `main` branch of any GitHub repository by passing a `--template` argument to the `create astro` command.

Run the following command in your terminal, substituting the official Astro starter template name, or the GitHub username and repository of the theme you want to use:

By default, this command will use the template repository’s `main` branch. To use a different branch name, pass it as part of the `--template` argument: `<github-username>/<github-repo>#<branch>`.

## Manual Setup

Section titled “Manual Setup”This guide will walk you through the steps to manually install and configure a new Astro project.

If you prefer not to use our automatic `create astro` CLI tool, you can set up your project yourself by following the guide below.

- 
Create your directory Create an empty directory with the name of your project, and then navigate into it. Once you are in your new directory, create your project `package.json`file. This is how you will manage your project dependencies, including Astro. If you aren’t familiar with this file format, run the following command to create one.
- 
Install Astro First, install the Astro project dependencies inside your project. Astro must be installed locally, not globally. Make sure you are *not*running`npm install -g astro``pnpm add -g astro`or`yarn add global astro`.Then, replace any placeholder “scripts” section of your `package.json`with the following:You’ll use these scripts later in the guide to start Astro and run its different commands. 
- 
Create your first page In your text editor, create a new file in your directory at `src/pages/index.astro`. This will be your first Astro page in the project.For this guide, copy and paste the following code snippet (including `---`dashes) into your new file:
- 
Create your first static asset You will also want to create a `public/`directory to store your static assets. Astro will always include these assets in your final build, so you can safely reference them from inside your component templates.In your text editor, create a new file in your directory at `public/robots.txt`.`robots.txt`is a simple file that most sites will include to tell search bots like Google how to treat your site.For this guide, copy and paste the following code snippet into your new file: 
- 
Create `astro.config.mjs`Astro is configured using `astro.config.mjs`. This file is optional if you do not need to configure Astro, but you may wish to create it now.Create `astro.config.mjs`at the root of your project, and copy the code below into it:If you want to include UI framework components such as React, Svelte, etc. or use other tools such as MDX or Partytown in your project, here is where you will manually import and configure integrations. Read Astro’s API configuration reference for more information.
- 
Add TypeScript support TypeScript is configured using `tsconfig.json`. Even if you don’t write TypeScript code, this file is important so that tools like Astro and VS Code know how to understand your project. Some features (like npm package imports) aren’t fully supported in the editor without a`tsconfig.json`file.If you do intend to write TypeScript code, using Astro’s `strict`or`strictest`template is recommended. You can view and compare the three template configurations at astro/tsconfigs/.Create `tsconfig.json`at the root of your project, and copy the code below into it. (You can use`base`,`strict`, or`strictest`for your TypeScript template):Read Astro’s TypeScript setup guide for more information.
- 
Next Steps If you have followed the steps above, your project directory should now look like this: - ## Directorynode_modules/- …
 
- ## Directorypublic/- robots.txt
 
- ## Directorysrc/- ## Directorypages/- index.astro
 
 
- astro.config.mjs
- package-lock.json or `yarn.lock`,`pnpm-lock.yaml`, etc.
- package.json
- tsconfig.json
 
- 
You can now start the Astro dev server and see a live preview of your project while you build!

# Citations

1. Source page: https://docs.astro.build/en/install-and-setup
