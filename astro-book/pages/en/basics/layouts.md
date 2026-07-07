---
type: Web Page
title: Layouts | Docs
description: An introduction to layouts in Astro.
resource: https://docs.astro.build/en/basics/layouts
timestamp: '2026-07-07T10:59:34.007706+00:00'
---

# Layouts

**Layouts** are Astro components used to provide a reusable UI structure, such as a page template.

We conventionally use the term “layout” for Astro components that provide common UI elements shared across pages such as headers, navigation bars, and footers. A typical Astro layout component provides Astro, Markdown or MDX pages with:

- a **page shell**(`<html>`,`<head>`and`<body>`tags)
- a `<slot />`

But, there is nothing special about a layout component! They can accept props and import and use other components like any other Astro component. They can include UI frameworks components and client-side scripts. They do not even have to provide a full page shell, and can instead be used as partial UI templates.

However, if a layout component does contain a page shell, its `<html>` element must be the parent of all other elements in the component.

Layout components are commonly placed in a `src/layouts` directory in your project for organization, but this is not a requirement; you can choose to place them anywhere in your project. You can even colocate layout components alongside your pages by prefixing the layout names with `_`.

## Sample Layout

Section titled “Sample Layout”## Using TypeScript with layouts

Section titled “Using TypeScript with layouts”Any Astro layout can be modified to introduce type safety & autocompletion by providing the types for your props:

## Markdown Layouts

Section titled “Markdown Layouts”Page layouts are especially useful for individual Markdown pages which otherwise would not have any page formatting.

Astro provides a special `layout` frontmatter property intended for individual `.md` files located within `src/pages/` using file-based routing to specify which `.astro` component to use as the page layout. This component allows you to provide `<head>` content like meta tags (e.g. `<meta charset="utf-8">`) and styles for the Markdown page. By default, this specified component can automatically access data from the Markdown file.

This is not recognized as a special property when using content collections to query and render your content.

A typical layout for a Markdown page includes:

- The `frontmatter`prop to access the Markdown page’s frontmatter and other data.
- A default `<slot />`to indicate where the page’s Markdown content should be rendered.

You can set a layout’s `Props` type with the `MarkdownLayoutProps` helper:

### Markdown Layout Props

Section titled “Markdown Layout Props”A Markdown layout will have access to the following information via `Astro.props`:

- `file`- `/home/user/projects/.../file.md`).
- `url`- `/en/guides/markdown-content`).
- `frontmatter`- `frontmatter.file`- `file`property.
- `frontmatter.url`- `url`property.
 
- `headings`- `h1 -> h6`) in the Markdown or MDX document with associated metadata. This list follows the type:- `{ depth: number; slug: string; text: string }[]`.
- `rawContent()`
- `compiledContent()`

A Markdown layout will have access to all the Markdown file’s available properties from `Astro.props` **with two key differences:**

- 
Heading information (i.e. `h1 -> h6`elements) is available via the`headings`array, rather than a`getHeadings()`function.
- 
`file`and`url`are*also*available as nested`frontmatter`properties (i.e.`frontmatter.url`and`frontmatter.file`).

### Importing Layouts Manually (MDX)

Section titled “Importing Layouts Manually (MDX)”You can also use the special Markdown layout property in the frontmatter of MDX files to pass `frontmatter` and `headings` props directly to a specified layout component in the same way.

To pass information to your MDX layout that does not (or cannot) exist in your frontmatter, you can instead import and use a `<Layout />` component. This works like any other Astro component, and will not receive any props automatically. Pass it any necessary props directly:

Then, your values are available to you through `Astro.props` in your layout, and your MDX content will be injected into the page where your `<slot />` component is written:

When using any layout (either through the frontmatter `layout` property or by importing a layout), you must include the `<meta charset="utf-8">` tag in your layout as Astro will no longer add it automatically to your MDX page.

## Nesting Layouts

Section titled “Nesting Layouts”Layout components do not need to contain an entire page worth of HTML. You can break your layouts into smaller components, and combine layout components to create even more flexible, page templates. This pattern is useful when you want to share some code across multiple layouts.

For example, a `BlogPostLayout.astro` layout component could style a post’s title, date and author. Then, a site-wide `BaseLayout.astro` could handle the rest of your page template, like navigation, footers, SEO meta tags, global styles, and fonts. You can also pass props received from your post to another layout, just like any other nested component.

# Citations

1. Source page: https://docs.astro.build/en/basics/layouts
