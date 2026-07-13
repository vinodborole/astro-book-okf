---
type: Web Page
title: Markdown in Astro | Docs
description: Learn about Astro's built-in support for Markdown.
resource: https://docs.astro.build/en/guides/markdown-content
timestamp: '2026-07-13T09:18:12.222139+00:00'
---

# Markdown in Astro

[Markdown](https://daringfireball.net/projects/markdown/) is commonly used to author text-heavy content like blog posts and documentation. Astro includes built-in support for Markdown files that can also include [frontmatter YAML](https://dev.to/paulasantamaria/introduction-to-yaml-125f) (or [TOML](https://toml.io)) to define custom properties such as a title, description, and tags.

In Astro, you can author content in [GitHub Flavored Markdown](https://github.github.com/gfm/), then render it in `.astro` components. This combines a familiar writing format designed for content with the flexibility of Astro’s component syntax and architecture.

For additional functionality, such as including components and JSX expressions in Markdown, add the [ @astrojs/mdx integration](/en/guides/integrations-guide/mdx/) to write your Markdown content using 

[MDX](https://mdxjs.com/).

## Organizing Markdown files

[Section titled “Organizing Markdown files”](#organizing-markdown-files)

Your local Markdown files can be kept anywhere within your `src/` directory. Markdown files located within `src/pages/` will automatically generate [Markdown pages on your site](#individual-markdown-pages).

Your Markdown content and frontmatter properties are available to use in components through [local file imports](#importing-markdown) or when [queried and rendered from data fetched by a content collections helper function](#markdown-from-content-collections-queries).

### File imports vs content collections queries

[Section titled “File imports vs content collections queries”](#file-imports-vs-content-collections-queries)

Local Markdown can be imported into `.astro` components using an `import` statement for a single file and [Vite’s  import.meta.glob()](/en/guides/imports/#importmetaglob) to query multiple files at once. The 

[exported data from these Markdown files](#importing-markdown)can then be used in the

`.astro` component.If you have groups of related Markdown files, consider [defining them as collections](/en/guides/content-collections/). This gives you several advantages, including the ability to store Markdown files anywhere on your filesystem or remotely.

Collections use content-specific, optimized APIs for [querying and rendering your Markdown content](#markdown-from-content-collections-queries) instead of file imports. Collections are intended for sets of data that share the same structure, such as blog posts or product items. When you define that shape in a schema, you additionally get validation, type safety, and Intellisense in your editor.

[when to use content collections](/en/guides/content-collections/#when-to-create-a-collection)instead of file imports.

## Dynamic JSX-like expressions

[Section titled “Dynamic JSX-like expressions”](#dynamic-jsx-like-expressions)

After importing or querying Markdown files, you can write dynamic HTML templates in your `.astro` components that include frontmatter data and body content.

### Available Properties

[Section titled “Available Properties”](#available-properties)

#### Markdown from content collections queries

[Section titled “Markdown from content collections queries”](#markdown-from-content-collections-queries)

When fetching data from your collections with the helper functions `getCollection()` or `getEntry()`, your Markdown’s frontmatter properties are available on a `data` object (e.g. `post.data.title`). Additionally, `body` contains the raw, uncompiled body content as a string.

The [ render()](/en/reference/modules/astro-content/#render) function returns your Markdown body content, a generated list of headings, as well as a modified frontmatter object after any Markdown plugins have been applied.

[using content returned by a collections query](/en/guides/content-collections/#using-content-in-astro-templates).

#### Importing Markdown

[Section titled “Importing Markdown”](#importing-markdown)

The following exported properties are available in your `.astro` component when importing Markdown using `import` or `import.meta.glob()`:

- `file`- `/home/user/projects/.../file.md`).
- `url`- `/en/guides/markdown-content`).
- `frontmatter`
- `<Content />`
- `rawContent()`
- `compiledContent()`
- `getHeadings()`- `<h1>`to- `<h6>`) in the file with the type:- `{ depth: number; slug: string; text: string }[]`. Each heading’s- `slug`corresponds to the generated ID for a given heading and can be used for anchor links.

An example Markdown blog post may pass the following `Astro.props` object:

## The `<Content />` Component

[Section titled “The <Content /> Component”](#the-content--component)

The `<Content />` component is available by importing `Content` from a Markdown file. This component returns the file’s full body content, rendered to HTML. You can optionally rename `Content` to any component name you prefer.

You can similarly [render the HTML content of a Markdown collection entry](/en/guides/content-collections/#rendering-body-content) by rendering a `<Content />` component.

## Heading IDs

[Section titled “Heading IDs”](#heading-ids)

Writing headings in Markdown will automatically give you anchor links so you can link directly to certain sections of your page.

Astro generates heading `id`s based on `github-slugger`. You can find more examples in [the github-slugger documentation](https://github.com/Flet/github-slugger#usage).

### Heading IDs and plugins

[Section titled “Heading IDs and plugins”](#heading-ids-and-plugins)

Astro injects an `id` attribute into all heading elements (`<h1>` to `<h6>`) in Markdown and MDX files. You can retrieve this data from the `getHeadings()` utility available as a [Markdown exported property](#available-properties) from an imported file, or from the `render()` function when [using Markdown returned from a content collections query](#markdown-from-content-collections-queries).

You can customize these heading IDs with a [Markdown processor](#choosing-a-markdown-processor) plugin that injects `id` attributes (e.g. `rehype-slug`). Your custom IDs, instead of Astro’s defaults, will be reflected in the HTML output and the items returned by `getHeadings()`.

Astro injects `id` attributes after your custom plugins have run, so any ID set by a plugin is preserved. If one of your custom plugins needs to access the IDs injected by Astro, you can import Astro’s heading ids plugin and place it before any plugins that rely on it:

## Markdown Plugins

[Section titled “Markdown Plugins”](#markdown-plugins)

Astro renders Markdown using a configurable **Markdown processor**. By default, this is [Sätteri](https://satteri.bruits.org/), Astro’s native Markdown and MDX pipeline, included with Astro.

Astro applies [GitHub-Flavored Markdown](https://github.github.com/gfm/) and [SmartyPants](https://daringfireball.net/projects/smartypants/) automatically. This brings some niceties like generating clickable links from text, and formatting for quotations and em-dashes.

You can extend Markdown processing with plugins, enable additional parser features, or [switch to a different processor entirely](#switching-to-the-unified-processor). See the full list of [Markdown configuration options](/en/reference/configuration-reference/#markdown-options).

### Choosing a Markdown processor

[Section titled “Choosing a Markdown processor”](#choosing-a-markdown-processor)

The [ markdown.processor option](/en/reference/configuration-reference/#markdownprocessor) controls which engine renders your 

`.md` and `.mdx` files. Astro provides two official options:- `satteri()`- [Sätteri](https://satteri.bruits.org/)pipeline, a fast Markdown and MDX compiler with its own plugin model. Included with Astro, so no extra installation is needed.
- `unified()`- [remark](https://remark.js.org/)and- [rehype](https://github.com/rehypejs/rehype)pipeline, with its large plugin ecosystem. Provided by- `@astrojs/markdown-remark`, which you install separately.

### Using Sätteri plugins and features

[Section titled “Using Sätteri plugins and features”](#using-sätteri-plugins-and-features)

The default `satteri()` processor accepts its own plugins through `mdastPlugins` and `hastPlugins`, and toggles optional parser features through `features`. See the [Sätteri documentation](https://satteri.bruits.org/docs/) for the available plugins and features.

Import `satteri` from `@astrojs/markdown-satteri` and pass your options to it through `markdown.processor`. This example adds an mdast plugin and enables the `directive` parser feature:

### Switching to the unified processor

[Section titled “Switching to the unified processor”](#switching-to-the-unified-processor)

To use [remark and rehype](https://unifiedjs.com/) instead of Sätteri, install `@astrojs/markdown-remark`, then import `unified` and pass it to `markdown.processor`:

Switching processors replaces Sätteri for both `.md` and `.mdx` files. Any Sätteri plugins in your config will not apply. To use remark and rehype only for `.mdx` files, set the [ processor option on the MDX integration](/en/guides/integrations-guide/mdx/#processor) instead.

#### Using remark and rehype plugins

[Section titled “Using remark and rehype plugins”](#using-remark-and-rehype-plugins)

The `unified()` processor accepts third-party [remark](https://github.com/remarkjs/remark) and [rehype](https://github.com/rehypejs/rehype) plugins. These plugins allow you to extend your Markdown with new capabilities, like [auto-generating a table of contents](https://github.com/remarkjs/remark-toc), [applying accessible emoji labels](https://github.com/florianeckerstorfer/remark-a11y-emoji), and [styling your Markdown](/en/guides/styling/#markdown-styling).

We encourage you to browse [awesome-remark](https://github.com/remarkjs/awesome-remark) and [awesome-rehype](https://github.com/rehypejs/awesome-rehype) for popular plugins! See each plugin’s own README for specific installation instructions.

After [switching to the  unified() processor](#switching-to-the-unified-processor), pass your plugins to it through 

`markdown.processor`. This example applies [and](https://github.com/remarkjs/remark-toc)

`remark-toc`[to Markdown files:](https://www.npmjs.com/package/rehype-accessible-emojis)

`rehype-accessible-emojis`#### Customizing a remark or rehype plugin

[Section titled “Customizing a remark or rehype plugin”](#customizing-a-remark-or-rehype-plugin)

In order to customize a plugin, provide an options object after it in a nested array.

The example below adds the [heading option to the  remarkToc plugin](https://github.com/remarkjs/remark-toc#options) to change where the table of contents is placed, and the 

[in order to add the anchor tag after the headline text.](https://github.com/rehypejs/rehype-autolink-headings#options)

`behavior` option to the `rehype-autolink-headings` plugin### Modifying frontmatter programmatically

[Section titled “Modifying frontmatter programmatically”](#modifying-frontmatter-programmatically)

When using the [remark/rehype processor](#using-remark-and-rehype-plugins), you can add frontmatter properties to all of your Markdown and MDX files with a remark or rehype plugin.

- 
Append a `customProperty`to the`data.astro.frontmatter`property from your plugin’s`file`argument:**Added in:**`astro@2.0.0``data.astro.frontmatter`contains all properties from a given Markdown or MDX document. This allows you to modify existing frontmatter properties, or compute new properties from this existing frontmatter.
- 
Apply this plugin to your `markdown`or`mdx`integration config:or 

Now, every Markdown or MDX file will have `customProperty` in its frontmatter, making it available when [importing your markdown](#importing-markdown) and from [the  Astro.props.frontmatter property in your layouts](#frontmatter-layout-property).

**Related recipe:**

[Add reading time](/en/recipes/reading-time/)

### Extending Markdown config from MDX

[Section titled “Extending Markdown config from MDX”](#extending-markdown-config-from-mdx)

Astro’s MDX integration will extend [your project’s existing Markdown configuration](/en/reference/configuration-reference/#markdown-options) by default, including the [Markdown processor](#choosing-a-markdown-processor). To override individual options, you can specify their equivalent in your MDX configuration.

The following example uses a different syntax highlighter and a different set of plugins for `.mdx` files than for `.md` files:

To avoid extending your Markdown config from MDX, set [the  extendMarkdownConfig option](/en/guides/integrations-guide/mdx/#extendmarkdownconfig) (enabled by default) to 

`false`:## Individual Markdown pages

[Section titled “Individual Markdown pages”](#individual-markdown-pages)

[Content collections](/en/guides/content-collections/) and [importing Markdown into  .astro components](#dynamic-jsx-like-expressions) provide more features for rendering your Markdown and are the recommended way to handle most of your content. However, there may be times when you want the convenience of just adding a file to 

`src/pages/` and having a simple page automatically created for you.Astro treats [any supported file inside of the  /src/pages/ directory](/en/basics/astro-pages/#supported-page-files) as a page, including 

`.md` and other Markdown file types.Placing a file in this directory, or any sub-directory, will automatically build a page route using the pathname of the file and display the Markdown content rendered to HTML. Astro will automatically add a `<meta charset="utf-8">` tag to your page to allow easier authoring of non-ASCII content.

### Frontmatter `layout` property

[Section titled “Frontmatter layout property”](#frontmatter-layout-property)

To help with the limited functionality of individual Markdown pages, Astro provides a special frontmatter `layout` property which is a relative path to an Astro [Markdown layout component](/en/basics/layouts/#markdown-layouts). `layout` is not a special property when using [content collections](/en/guides/content-collections/) to query and render your Markdown content, and is not guaranteed to be supported outside of its intended use case.

If your Markdown file is located within `src/pages/`, create a layout component and add it in this layout property to provide a page shell around your Markdown content.

This layout component is a regular Astro component with [specific properties automatically available](/en/basics/layouts/#markdown-layout-props) through `Astro.props` for your Astro template. For example, you can access your Markdown file’s frontmatter properties through `Astro.props.frontmatter`:

When using the frontmatter `layout` property, you must include the `<meta charset="utf-8">` tag in your layout as Astro will no longer add it automatically. You can now also [style your Markdown](/en/guides/styling/#markdown-styling) in your layout component.

[Markdown Layouts](/en/basics/layouts/#markdown-layouts).

## Fetching Remote Markdown

[Section titled “Fetching Remote Markdown”](#fetching-remote-markdown)

Astro’s internal Markdown processor is not available for processing remote Markdown.

To fetch remote Markdown for use in [content collections](/en/guides/content-collections/), you can [build a custom loader](/en/guides/content-collections/#custom-build-time-loaders) with access to a [ renderMarkdown() function](/en/reference/content-loader-reference/#loadercontextrendermarkdown).

To fetch remote Markdown directly and render it to HTML, you will need to install and configure your own Markdown parser from NPM. This will not inherit from any of Astro’s built-in Markdown settings that you have configured.

Be sure that you understand these limitations before implementing this in your project, and consider fetching your remote Markdown using a content collections loader instead.

Learn[Contribute](/en/contribute/)

[Community](https://astro.build/chat)

[Sponsor](https://opencollective.com/astrodotbuild)

# Citations

1. Source page: https://docs.astro.build/en/guides/markdown-content
