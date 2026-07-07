---
type: Web Page
title: Syntax Highlighting | Docs
description: Learn how to highlight your code blocks in Astro.
resource: https://docs.astro.build/en/guides/syntax-highlighting
timestamp: '2026-07-07T10:59:34.007706+00:00'
---

# Syntax Highlighting

Astro comes with built-in support for Shiki and Prism. This provides syntax highlighting for:

- all code fences (```) used in a Markdown or MDX file.
- content within the built-in `<Code />`component (powered by Shiki) in`.astro`files.
- content within the `<Prism />`component (powered by Prism) in`.astro`files.

Add community integrations such as Expressive Code for even more text marking and annotation options in your code blocks.

## Markdown code blocks

Section titled “Markdown code blocks”A Markdown code block is indicated by a block with three backticks ``` at the start and end. You can indicate the programming language being used after the opening backticks to indicate how to color and style your code to make it easier to read.

Astro’s Markdown code blocks are styled by Shiki by default, preconfigured with the `github-dark` theme. The compiled output will be limited to inline `style`s without any extraneous CSS classes, stylesheets, or client-side JS.

You can add a Prism stylesheet and switch to Prism’s highlighting, or disable Astro’s syntax highlighting entirely, with the `markdown.syntaxHighlight` configuration option.

`markdown.shikiConfig` reference for the complete set of Markdown syntax highlighting options available when using Shiki.
### Setting a default Shiki theme

Section titled “Setting a default Shiki theme”You can configure any built-in Shiki theme for your Markdown code blocks in your Astro config:

### Setting light and dark mode themes

Section titled “Setting light and dark mode themes”You can specify dual Shiki themes for light and dark mode in your Astro config:

Then, add Shiki’s dark mode CSS variables via media query or classes to apply to all your Markdown code blocks by default. Replace the `.shiki` class in the examples from Shiki’s documentation with `.astro-code`:

### Adding your own Shiki theme

Section titled “Adding your own Shiki theme”Instead of using one of Shiki’s predefined themes, you can import a custom Shiki theme from a local file.

### Customizing Shiki themes

Section titled “Customizing Shiki themes”You can follow Shiki’s own theme documentation for more customization options for themes, light vs dark mode toggles, or styling via CSS variables.

You will need to adjust the examples from Shiki’s documentation for your Astro project by making the following substitutions:

- Code blocks are styled using the `.astro-code`class instead of`.shiki`
- When using the `css-variables`theme, custom properties are prefixed with`--astro-code-`instead of`--shiki-`

## Components for code blocks

Section titled “Components for code blocks”There are two Astro components available for `.astro` and `.mdx` files to render code blocks: `<Code />` and `<Prism />`.

You can reference the `Props` of these components using the `ComponentProps` type utility.

`<Code />`

Section titled “<Code />”This component is powered internally by Shiki. It supports all popular Shiki themes and languages as well as several other Shiki options such as custom themes, languages, transformers, and default colors.

These values are passed to the `<Code />` component using the `theme`, `lang`, `embeddedLangs`, `transformers`, and `defaultColor` attributes respectively as props. The `<Code />` component will not inherit your `shikiConfig` settings for Markdown code blocks.

`embeddedLangs`

Section titled “embeddedLangs”**Type:** `string[] | undefined`

**Added in:**

`astro@6.0.0`
	
	
Any additional languages to be included for syntax highlighting by Shiki.

A `lang` value may include support for highlighting some additional languages by default (e.g. `lang="svelte"` will also provide highlighting for `ts`).

Use `embeddedLangs` to include support for additional, non-standard language combinations (e.g. `jsx` support when `lang="vue"`).

`transformers`

Section titled “transformers”**Type:** `ShikiTransformer[] | undefined`

**Added in:**

`astro@4.11.0`
	
	
An array of Shiki transformers to be applied to your `code`. Since Astro v4.14.0, you can also provide a string for Shiki’s `meta` attribute to pass options to transformers.

Note that `transformers` only applies classes and you must provide your own CSS rules to target the elements of your code block.

`<Prism />`

Section titled “<Prism />”This component provides language-specific syntax highlighting for code blocks by applying Prism’s CSS classes. Note that you must provide a Prism CSS stylesheet (or bring your own) to style the classes.

To use the `Prism` highlighter component, you must install the `@astrojs/prism` package:

Then, you can import and use the `<Prism />` component like any other Astro component, passing a language and the code to render.

In addition to the list of languages supported by Prism, you can also use `lang="astro"` to display Astro code blocks.

## Add a Prism stylesheet

Section titled “Add a Prism stylesheet”If you opt to use Prism (either by configuring `markdown.syntaxHighlight: 'prism'` or with the `<Prism />` component), Astro will apply Prism’s CSS classes instead of Shiki’s to your code. You will need to bring your own CSS stylesheet for syntax highlighting to appear.

- 
Choose a premade stylesheet from the available Prism Themes. 
- 
Add this stylesheet to your project’s `public/`directory.
- 
Load this into your page’s `<head>`in a layout component via a`<link>`tag. (See Prism basic usage.)

You can also visit the list of languages supported by Prism for options and usage.

Learn

# Citations

1. Source page: https://docs.astro.build/en/guides/syntax-highlighting
