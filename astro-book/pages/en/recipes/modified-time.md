---
type: Web Page
title: Add last modified time | Docs
description: Build a remark plugin to add the last modified time to your Markdown
  and MDX.
resource: https://docs.astro.build/en/recipes/modified-time
timestamp: '2026-07-07T10:59:34.007706+00:00'
---

# Add last modified time

Learn how to build a remark plugin that adds the last modified time as a custom frontmatter property of your Markdown and MDX files. Use this property to display the modified time in your pages.

This recipe calculates time based on your repository’s Git history and may not be accurate on some deployment platforms. Your host may be performing **shallow clones** which do not retrieve the full git history.

## Recipe

Section titled “Recipe”- 
Install `Day.js`to modify and format times, and`@astrojs/markdown-remark`to use the`unified()`processor:
- 
Create a Remark Plugin This plugin uses `execSync`to run a Git command that returns the timestamp of the latest commit in ISO 8601 format. The timestamp is then added to the frontmatter of the file.## Using the file system instead of GitAlthough using Git is the recommended way to get the last modified timestamp from a file, it is possible to use the file system modified time. This plugin uses `statSync`to get the`mtime`(modified time) of the file in ISO 8601 format. The timestamp is then added to the frontmatter of the file.
- 
Add the plugin to your config Now all Markdown documents will have a `lastModified`property in their frontmatter.
- 
Display Last Modified Time If your content is stored in a content collection, access the `remarkPluginFrontmatter`from the`render(entry)`function. Then render`lastModified`in your template wherever you would like it to appear.If you’re using a Markdown layout, use the `lastModified`frontmatter property from`Astro.props`in your layout template.

# Citations

1. Source page: https://docs.astro.build/en/recipes/modified-time
