---
type: Web Page
title: Use Bun with Astro | Docs
description: Learn how to use Bun with your Astro site.
resource: https://docs.astro.build/en/recipes/bun
timestamp: '2026-08-03T09:35:37.104348+00:00'
---

# Use Bun with Astro

[Bun](https://bun.sh/) is an all-in-one JavaScript runtime & toolkit. See [Bun’s documentation](https://bun.sh/docs) for more information.

Using Bun with Astro may reveal rough edges. Some integrations may not work as expected. Consult [Bun’s official documentation for working with Astro](https://bun.sh/guides/ecosystem/astro) for details.

If you have any problems using Bun, please [open an Issue on GitHub with Bun directly](https://github.com/oven-sh/bun/issues/new/choose).

## Prerequisites

[Section titled “Prerequisites”](#prerequisites)

- Bun installed locally on your machine. See the [installation instructions](https://bun.sh/docs/installation) in Bun’s official documentation.

## Create a new Astro project with Bun

[Section titled “Create a new Astro project with Bun”](#create-a-new-astro-project-with-bun)

Create a new Astro project with Bun using the following `create-astro` command:

## Install dependencies

[Section titled “Install dependencies”](#install-dependencies)

If you skipped the “Install dependencies?” step during the CLI wizard, then be sure to install your dependencies before continuing.

## Add Types

[Section titled “Add Types”](#add-types)

Bun publishes the [`@types/bun`](https://www.npmjs.com/package/@types/bun) package, containing the runtime types for Bun.

Install `@types/bun` using the following command:

## CLI installation flags

[Section titled “CLI installation flags”](#cli-installation-flags)

### Using integrations

[Section titled “Using integrations”](#using-integrations)

You can also use any of the official Astro integrations with the `astro add` command:

### Use a theme or starter template

[Section titled “Use a theme or starter template”](#use-a-theme-or-starter-template)

You can start a new Astro project based on an [official example](https://github.com/withastro/astro/tree/main/examples) or the main branch of any GitHub repository by passing a `--template` argument to the `create astro` command.

Run the following command in your terminal, substituting the official Astro starter template name, or the GitHub username and repository of the theme you want to use:

## Develop and build

[Section titled “Develop and build”](#develop-and-build)

To run the development server, use following command:

### Build and preview your site

[Section titled “Build and preview your site”](#build-and-preview-your-site)

To build your site, use the following command:

When the build is finished, run the appropriate preview command (e.g. `bun run preview`) in your terminal and you can view the built version of your site locally in the same browser preview window.

## Testing

[Section titled “Testing”](#testing)

Bun ships with a fast, built-in, Jest-compatible test runner through the [`bun test` command](https://bun.sh/docs/cli/test). You can also use any other [testing tools for Astro](/en/guides/testing/).

## Official Resources

[Section titled “Official Resources”](#official-resources)

## Community Resources

[Section titled “Community Resources”](#community-resources)

Using Bun with Astro? Add your blog post or video to this page!

- [Using Bun with Astro and Cloudflare Pages](https://handerson.hashnode.dev/using-bun-with-astro-and-cloudflare-pages) - blog post

[Contribute](/en/contribute/)

[Community](https://astro.build/chat)

[Sponsor](https://opencollective.com/astrodotbuild)

# Citations

1. Source page: https://docs.astro.build/en/recipes/bun
