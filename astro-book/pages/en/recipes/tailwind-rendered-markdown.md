---
type: Web Page
title: Style rendered Markdown with Tailwind Typography | Docs
description: Learn how to use @tailwind/typography to style your rendered Markdown.
resource: https://docs.astro.build/en/recipes/tailwind-rendered-markdown
timestamp: '2026-08-03T09:35:37.104348+00:00'
---

# Style rendered Markdown with Tailwind Typography

You can use [Tailwind](https://tailwindcss.com)’s Typography plugin to style rendered Markdown from sources such as Astro’s [**content collections**](/en/guides/content-collections/).

This recipe will teach you how to create a reusable Astro component to style your Markdown content using Tailwind’s utility classes.

## Prerequisites

[Section titled “Prerequisites”](#prerequisites)

An Astro project that:

- has [Tailwind’s Vite plugin](/en/guides/styling/#tailwind) installed.
- uses Astro’s [content collections](/en/guides/content-collections/) .

## Setting Up `@tailwindcss/typography`

[Section titled “Setting Up @tailwindcss/typography”](#setting-up-tailwindcsstypography)

First, install `@tailwindcss/typography` using your preferred package manager.

Then, add the package as a plugin in your Tailwind configuration file.

## Recipe

[Section titled “Recipe”](#recipe)

1. 
Create a `<Prose />` component to provide a wrapping`<div>` with a`<slot />` for your rendered Markdown. Add the style class`prose` alongside any desired[Tailwind element modifiers](https://tailwindcss.com/docs/typography-plugin#element-modifiers) in the parent element.The `@tailwindcss/typography` plugin uses[**element modifiers**](https://tailwindcss.com/docs/typography-plugin#element-modifiers) to style child components of a container with the`prose` class.These modifiers follow the following general syntax: For example, `prose-h1:font-bold` gives all`<h1>` tags the`font-bold` Tailwind class.
2. 
Query your collection entry on the page you want to render your Markdown. Pass the `<Content />` component from`await render(entry)` to`<Prose />` as a child to wrap your Markdown content in Tailwind styles.

## Resources

[Section titled “Resources”](#resources)

[Contribute](/en/contribute/)

[Community](https://astro.build/chat)

[Sponsor](https://opencollective.com/astrodotbuild)

# Citations

1. Source page: https://docs.astro.build/en/recipes/tailwind-rendered-markdown
