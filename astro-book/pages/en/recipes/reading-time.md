---
type: Web Page
title: Add reading time | Docs
description: Build a remark plugin to add reading time to your Markdown or MDX files.
resource: https://docs.astro.build/en/recipes/reading-time
timestamp: '2026-08-03T09:35:37.104348+00:00'
---

# Add reading time

Create a [remark plugin](https://github.com/remarkjs/remark) which adds a reading time property to the frontmatter of your Markdown or MDX files. Use this property to display the reading time for each page.

## Recipe

[Section titled “Recipe”](#recipe)

1. 
Install the following packages: 
  - [`reading-time`](https://www.npmjs.com/package/reading-time) to calculate minutes read
  - [`mdast-util-to-string`](https://www.npmjs.com/package/mdast-util-to-string) to extract all text from your markdown
  - [`@astrojs/markdown-remark`](https://www.npmjs.com/package/@astrojs/markdown-remark) to use[the `unified()` processor](/en/guides/markdown-content/#using-remark-and-rehype-plugins) :
2. 
Create a remark plugin. This plugin uses the `mdast-util-to-string` package to get the Markdown file’s text. This text is then passed to the`reading-time` package to calculate the reading time in minutes.
3. 
Add the plugin to your config: Now all Markdown documents will have a calculated `minutesRead` property in their frontmatter.
4. 
Display Reading Time If your blog posts are stored in a [content collection](/en/guides/content-collections/) , access the`remarkPluginFrontmatter` from the`render(entry)` function. Then, render`minutesRead` in your template wherever you would like it to appear.If you’re using a [Markdown layout](/en/basics/layouts/#markdown-layouts) , use the`minutesRead` frontmatter property from`Astro.props` in your layout template.

[Contribute](/en/contribute/)

[Community](https://astro.build/chat)

[Sponsor](https://opencollective.com/astrodotbuild)

# Citations

1. Source page: https://docs.astro.build/en/recipes/reading-time
