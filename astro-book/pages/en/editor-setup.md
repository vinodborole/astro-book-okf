---
type: Web Page
title: Editor setup | Docs
description: Set up your code editor to build with Astro.
resource: https://docs.astro.build/en/editor-setup
timestamp: '2026-07-07T10:59:34.007706+00:00'
---

# Editor setup

Customize your code editor to improve the Astro developer experience and unlock new features.

## VS Code

Section titled “VS Code”VS Code is a popular code editor for web developers, built by Microsoft. The VS Code engine also powers popular in-browser code editors like GitHub Codespaces.

Astro works with any code editor. However, VS Code is our recommended editor for Astro projects. We maintain an official Astro VS Code Extension that unlocks several key features and developer experience improvements for Astro projects.

- Syntax highlighting for `.astro`files.
- TypeScript type information for `.astro`files.
- VS Code Intellisense for code completion, hints and more.

To get started, install the Astro VS Code Extension today.

Zed is a high-performance, multiplayer code editor that is optimized for speed and large projects. Their Astro extension includes features like syntax highlighting for `.astro` files, code completion, formatting, diagnostics, and go-to-definition.

## JetBrains IDEs

Section titled “JetBrains IDEs”Webstorm is a JavaScript and TypeScript IDE that added support for the Astro Language Server in version 2024.2. This update brings features like syntax highlighting, code completion, and formatting.

Install the official plugin through JetBrains Marketplace or by searching for “Astro” in the IDE’s Plugins tab. You can toggle the language server in `Settings | Languages & Frameworks | TypeScript | Astro`.

For more information on Astro support in Webstorm, check out the official Webstorm Astro Documentation.

## Other Code Editors

Section titled “Other Code Editors”Our amazing community maintains several extensions for other popular editors, including:

- VS Code Extension on Open VSX Official - The official Astro VS Code Extension, available on the Open VSX registry for editors like Cursor or VSCodium.
- Vim Plugin Community - Provides syntax highlighting, indentation, and code folding support for Astro inside of Vim or Neovim
- Neovim LSP and TreeSitter Plugins Community - Provides syntax highlighting, treesitter parsing, and code completion for Astro inside of Neovim
- Emacs - See instructions for Configuring Emacs and Eglot Community to work with Astro
- Astro syntax highlighting for Sublime Text Community - The Astro package for Sublime Text, available on the Sublime Text package manager.
- Nova Extension Community - Provides syntax highlighting and code completion for Astro inside of Nova

## In-Browser Editors

Section titled “In-Browser Editors”In addition to local editors, Astro also runs well on in-browser hosted editors, including:

- StackBlitz and CodeSandbox - online editors that run in your browser, with built-in syntax highlighting support for `.astro`files. No installation or configuration required!
- GitHub.dev - allows you to install the Astro VS Code extension as a web extension, which gives you access to only some of the full extension features. Currently, only syntax highlighting is supported.

## Other tools

Section titled “Other tools”### ESLint

Section titled “ESLint”ESLint is a popular linter for JavaScript and JSX. For Astro support, a community maintained plugin can be installed.

See the project’s User Guide for more information on how to install and set up ESLint for your project.

### Stylelint

Section titled “Stylelint”Stylelint is a popular linter for CSS. A community maintained Stylelint configuration provides Astro support.

Installation instructions, editor integration, and additional information can be found in the project’s README.

Biome is an all-in-one linter and formatter for the web. Biome currently has experimental support for `.astro` files, and can be used to lint and format the frontmatter in `.astro` files.

### Prettier

Section titled “Prettier”Prettier is a popular formatter for JavaScript, HTML, CSS, and more. If you’re using the Astro VS Code Extension, code formatting with Prettier is included.

To add support for formatting `.astro` files outside of the editor (e.g. CLI) or inside editors that don’t support our editor tooling, install the official Astro Prettier plugin.

- 
Install `prettier`and`prettier-plugin-astro`.
- 
Create a `.prettierrc`configuration file (or`.prettierrc.json`,`.prettierrc.mjs`, or other supported formats) in the root of your project and add`prettier-plugin-astro`to it.In this file, also manually specify the parser for Astro files. 
- 
Optionally, install other Prettier plugins for your project, and add them to the configuration file. These additional plugins may need to be listed in a specific order. For example, if you use Tailwind, `prettier-plugin-tailwindcss`must be the last Prettier plugin in the plugins array.
- 
Run the following command in your terminal to format your files. 

See the Prettier plugin’s README for more information about its supported options, how to set up Prettier inside VS Code, and more.

### dprint

Section titled “dprint”dprint is a highly-configurable code formatter that supports many languages, including JavaScript, TypeScript, CSS, and more. Support for `.astro` files can be added using the markup_fmt plugin.

# Citations

1. Source page: https://docs.astro.build/en/editor-setup
