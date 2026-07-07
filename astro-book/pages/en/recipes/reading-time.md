---
type: Web Page
title: Add reading time | Docs
description: Build a remark plugin to add reading time to your Markdown or MDX files.
resource: https://docs.astro.build/en/recipes/reading-time
timestamp: '2026-07-07T10:59:34.007706+00:00'
---

# Add reading time

Create a remark plugin which adds a reading time property to the frontmatter of your Markdown or MDX files. Use this property to display the reading time for each page.

## Recipe

Section titled “Recipe”- 
Install the following packages: - `reading-time`to calculate minutes read
- `mdast-util-to-string`to extract all text from your markdown
- `@astrojs/markdown-remark`to use the- `unified()`processor:
 
- 
Create a remark plugin. This plugin uses the `mdast-util-to-string`package to get the Markdown file’s text. This text is then passed to the`reading-time`package to calculate the reading time in minutes.
- 
Add the plugin to your config: Now all Markdown documents will have a calculated `minutesRead`property in their frontmatter.
- 
Display Reading Time If your blog posts are stored in a content collection, access the `remarkPluginFrontmatter`from the`render(entry)`function. Then, render`minutesRead`in your template wherever you would like it to appear.If you’re using a Markdown layout, use the `minutesRead`frontmatter property from`Astro.props`in your layout template.

# Citations

1. Source page: https://docs.astro.build/en/recipes/reading-time
