---
type: Web Page
title: Using custom fonts | Docs
description: Looking to add some custom typefaces to an Astro website? Use Google
  Fonts with Fontsource or add a font of your choice.
resource: https://docs.astro.build/en/guides/fonts
timestamp: '2026-07-13T09:18:12.222139+00:00'
---

# Using custom fonts

This guide will show you how to add [web fonts](https://developer.mozilla.org/en-US/docs/Learn/CSS/Styling_text/Web_fonts) to your project and use them in your components.

Astro provides a way to use fonts from your filesystem and various font providers (e.g. Fontsource, Google) through a unified, [fully customizable](/en/reference/configuration-reference/#fonts), and type-safe API.

Web fonts can impact page performance at both load time and rendering time. This API helps you keep your site performant with automatic [web font optimizations](https://web.dev/learn/performance/optimize-web-fonts) including preload links, optimized fallbacks, and opinionated defaults. [See common usage examples](#examples).

The Fonts API focuses on performance and privacy by downloading and caching fonts so they’re served from your site. This can avoid sending user data to third-party sites, and also ensures that a consistent set of fonts is available to all your visitors.

## Configuring custom fonts

[Section titled “Configuring custom fonts”](#configuring-custom-fonts)

Registering custom fonts for your Astro project is done through [the  fonts option](/en/reference/configuration-reference/#fonts) in your Astro config.

For each font you want to use, you must specify its [name](/en/reference/configuration-reference/#fontname), a [CSS variable](/en/reference/configuration-reference/#fontcssvariable), and an Astro font provider.

Astro provides [built-in support for the most popular font providers](/en/reference/font-provider-reference/#built-in-providers): Adobe, Bunny, Fontshare, Fontsource, Google, Google Icons and NPM, as well as for using your own local font files. Additionally, you can [further customize your font configuration](#granular-font-configuration) to optimize performance and visitor experience.

### Using a local font file

[Section titled “Using a local font file”](#using-a-local-font-file)

This example will demonstrate adding a custom font using the font file `DistantGalaxy.woff2`.

- 
Add your font file inside the `src/`directory`src/assets/fonts/`.
- 
Create a new font family in your Astro config file using the [local font provider](/en/reference/font-provider-reference/#local)and specify the variants to be included:
- 
Your font is now configured and ready to be [added to your page head](#applying-custom-fonts)so that it can be used in your project.

### Using Fontsource

[Section titled “Using Fontsource”](#using-fontsource)

Astro supports [several font providers](/en/reference/font-provider-reference/#built-in-providers) out of the box, including support for [Fontsource](https://fontsource.org/) that simplifies using Google Fonts and other open-source fonts.

The following example will use Fontsource to add custom font support, but the process is similar for any of Astro’s built-in font providers (e.g. [Adobe](https://fonts.adobe.com/), [Bunny](https://fonts.bunny.net/)).

- 
Find the font you want to use in [Fontsource’s catalog](https://fontsource.org/). This example will use[Roboto](https://fontsource.org/fonts/roboto).
- 
Create a new font family in your Astro config file using the [Fontsource provider](/en/reference/font-provider-reference/#fontsource):
- 
Your font is now configured and ready to be [added to your page head](#applying-custom-fonts)so that it can be used in your project.

## Applying custom fonts

[Section titled “Applying custom fonts”](#applying-custom-fonts)

After [a font is configured](#configuring-custom-fonts), it must be added to your page head with an identifying CSS variable. Then, you can use this variable when defining your page styles.

- 
Import and include the `<Font />``cssVariable`property in the head of your page, usually in a dedicated`Head.astro`component or in a[layout](/en/basics/layouts/)component directly:
- 
In any page rendered with that layout, including the layout component itself, you can now define styles with your font’s `cssVariable`to apply your custom font.In the following example, the `<h1>`heading will have the custom font applied, while the paragraph`<p>`will not.

## Preloading fonts

[Section titled “Preloading fonts”](#preloading-fonts)

Font preloading should be done sparingly, as it can block the loading of other important resources or download fonts that are unnecessary for the current page. Consider preloading only the most essential fonts, necessary for displaying content visible above the fold.

To preload a font, pass the [ preload property](/en/reference/modules/astro-assets/#preload) to the corresponding 

`<Font />` component. If multiple files correspond to a font, you can also specify which one to preload by passing an array.## Register fonts in Tailwind

[Section titled “Register fonts in Tailwind”](#register-fonts-in-tailwind)

If you are using [Tailwind](/en/guides/styling/#tailwind) for styling, you will not apply your styles with the `font-face` CSS property.

Instead, after [configuring your custom font](#configuring-custom-fonts) and [adding it to your page head](#applying-custom-fonts), you will need to update your Tailwind configuration to register your font:

See [Tailwind’s docs on adding custom font families](https://tailwindcss.com/docs/font-family#using-a-custom-value) for more information.

## Using variable fonts

[Section titled “Using variable fonts”](#using-variable-fonts)

To use [variable fonts](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_fonts/Variable_fonts_guide) in your project, specify the available weight range instead of individual weights in your provider’s configuration.

When [using a local font file](#using-a-local-font-file), you can specify that the font is variable by setting the [ weight property of the variant](/en/reference/font-provider-reference/#weight) to a string corresponding to the exact weight range available for the font.

The following example configures Inter as a local variable font with the available weight range:

When using [other providers (e.g. Fontsource)](#using-fontsource), that support variable fonts, you can request the variable version of a font by setting the [ weights property](/en/reference/configuration-reference/#fontweights) with an array containing the exact range of weights available for the font.

The following example downloads [Fira Code from Fontsource](https://fontsource.org/fonts/fira-code) as a variable font with the available weight range:

## Customizing font fallbacks

[Section titled “Customizing font fallbacks”](#customizing-font-fallbacks)

Fallback fonts are used when the primary font has not yet loaded, contains missing characters, or cannot be loaded for any reason. When the fallback font differs significantly from the primary font, layout shifts may occur during page loading.

To avoid this, Astro automatically tries to generate optimized fallback fonts from the last [defined fallback](/en/reference/configuration-reference/#fontfallbacks) if it is a [generic font family](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/font-family#generic-name). It uses `sans-serif` by default, but it may not match the desired appearance of your primary font. You can adjust it in your font configuration:

You can also opt out of the default optimization by setting [ font.optimizedFallbacks](/en/reference/configuration-reference/#fontoptimizedfallbacks) to 

`false` in your font configuration. Astro will then use the fallback fonts specified in your configuration without any additional automatic processing.## Accessing font data programmatically

[Section titled “Accessing font data programmatically”](#accessing-font-data-programmatically)

Astro exposes low-level APIs for accessing data programmatically:

- Font family data through the `fontData`
- Font file URLs with the `experimental_getFontFileURL()`

This can be useful for advanced use cases where you need direct access to font files, such as generating OpenGraph images with [Satori](https://github.com/vercel/satori) in an [API Route](/en/guides/endpoints/#server-endpoints-api-routes).

The `fontData` object gives you access to all font files downloaded by Astro for your project, along with their metadata. This means that you are responsible for filtering font files to find the specific file you need, and for fetching data after resolving URLs.

The following example generates an OpenGraph image in a static file endpoint, assuming that only [one font and its format have been configured](/en/reference/configuration-reference/#fontformats) with a [format supported by Satori](https://github.com/vercel/satori?tab=readme-ov-file#fonts):

## Granular font configuration

[Section titled “Granular font configuration”](#granular-font-configuration)

A font family is defined by a combination of properties such as weights and styles (e.g. `weights: [500, 600]` and `styles: ["normal", "bold"]`), but you may want to download only certain combinations of these.

For greater control over which font files are downloaded, you can specify the same font (ie. with the same `cssVariable`, `name`, and `provider` properties) multiple times with different combinations. Astro will merge the results and download only the required files. For example, it is possible to download normal `500` and `600` while downloading only italic `500`:

## Caching

[Section titled “Caching”](#caching)

The Fonts API caching implementation was designed to be practical in development and efficient in production. During builds, font files are copied to the `_astro/fonts` output directory, so they can benefit from HTTP caching of static assets (usually a year).

To clear the cache in development, remove the `.astro/fonts` directory. To clear the build cache, remove the `node_modules/.astro/fonts` directory.

## Examples

[Section titled “Examples”](#examples)

Astro’s font feature is based on flexible configuration options. Your own project’s font configuration may look different from simplified examples, so the following are provided to show what various font configurations might look like when used in production.

Learn[Contribute](/en/contribute/)

[Community](https://astro.build/chat)

[Sponsor](https://opencollective.com/astrodotbuild)

# Citations

1. Source page: https://docs.astro.build/en/guides/fonts
