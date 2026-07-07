---
type: Web Page
title: Style rendered Markdown with Tailwind Typography | Docs
description: Learn how to use @tailwind/typography to style your rendered Markdown.
resource: https://docs.astro.build/en/recipes/tailwind-rendered-markdown
timestamp: '2026-07-07T10:59:34.007706+00:00'
---

# Style rendered Markdown with Tailwind Typography

You can use Tailwind’s Typography plugin to style rendered Markdown from sources such as Astro’s **content collections**.

This recipe will teach you how to create a reusable Astro component to style your Markdown content using Tailwind’s utility classes.

## Prerequisites

Section titled “Prerequisites”An Astro project that:

- has Tailwind’s Vite plugin installed.
- uses Astro’s content collections.

## Setting Up `@tailwindcss/typography`

Section titled “Setting Up @tailwindcss/typography”First, install `@tailwindcss/typography` using your preferred package manager.

Then, add the package as a plugin in your Tailwind configuration file.

## Recipe

Section titled “Recipe”- 
Create a `<Prose />`component to provide a wrapping`<div>`with a`<slot />`for your rendered Markdown. Add the style class`prose`alongside any desired Tailwind element modifiers in the parent element.The `@tailwindcss/typography`plugin uses**element modifiers**to style child components of a container with the`prose`class.These modifiers follow the following general syntax: For example, `prose-h1:font-bold`gives all`<h1>`tags the`font-bold`Tailwind class.
- 
Query your collection entry on the page you want to render your Markdown. Pass the `<Content />`component from`await render(entry)`to`<Prose />`as a child to wrap your Markdown content in Tailwind styles.

# Citations

1. Source page: https://docs.astro.build/en/recipes/tailwind-rendered-markdown
