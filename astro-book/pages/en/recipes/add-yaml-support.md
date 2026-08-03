---
type: Web Page
title: Installing a Vite or Rollup plugin | Docs
description: Learn how you can import YAML data by adding a Rollup plugin to your
  project.
resource: https://docs.astro.build/en/recipes/add-yaml-support
timestamp: '2026-08-03T09:35:37.104348+00:00'
---

# Installing a Vite or Rollup plugin

Astro builds on top of Vite, and supports both Vite and Rollup plugins. This recipe uses a Rollup plugin to add the ability to import a YAML (`.yml`) file in Astro.

## Recipe

[Section titled “Recipe”](#recipe)

1. 
Install `@rollup/plugin-yaml` :
2. 
Import the plugin in your `astro.config.mjs` and add it to the Vite plugins array:
3. 
Finally, you can import YAML data using an `import` statement:While you can now import YAML data in your Astro project, your editor will not provide types for the imported data. To add types, create or find an existing `*.d.ts` file in the`src` directory of your project and add the following:This will allow your editor to provide type hints for your YAML data.

[Contribute](/en/contribute/)

[Community](https://astro.build/chat)

[Sponsor](https://opencollective.com/astrodotbuild)

# Citations

1. Source page: https://docs.astro.build/en/recipes/add-yaml-support
