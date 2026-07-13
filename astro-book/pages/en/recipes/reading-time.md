---
type: Web Page
title: Add reading time | Docs
description: Build a remark plugin to add reading time to your Markdown or MDX files.
resource: https://docs.astro.build/en/recipes/reading-time
timestamp: '2026-07-13T09:18:12.222139+00:00'
---

# Add reading time

Create a [remark plugin](https://github.com/remarkjs/remark) which adds a reading time property to the frontmatter of your Markdown or MDX files. Use this property to display the reading time for each page.

## Recipe

[Section titled “Recipe”](#recipe)

- 
Install the following packages: - `reading-time`
- `mdast-util-to-string`
- `@astrojs/markdown-remark`- [the](/en/guides/markdown-content/#using-remark-and-rehype-plugins):- `unified()`processor
 
- 
Create a remark plugin. This plugin uses the `mdast-util-to-string`package to get the Markdown file’s text. This text is then passed to the`reading-time`package to calculate the reading time in minutes.
- 
Add the plugin to your config: Now all Markdown documents will have a calculated `minutesRead`property in their frontmatter.
- 
Display Reading Time If your blog posts are stored in a [content collection](/en/guides/content-collections/), access the`remarkPluginFrontmatter`from the`render(entry)`function. Then, render`minutesRead`in your template wherever you would like it to appear.If you’re using a [Markdown layout](/en/basics/layouts/#markdown-layouts), use the`minutesRead`frontmatter property from`Astro.props`in your layout template.

[Contribute](/en/contribute/)

[Community](https://astro.build/chat)

[Sponsor](https://opencollective.com/astrodotbuild)

# Citations

1. Source page: https://docs.astro.build/en/recipes/reading-time
