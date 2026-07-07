---
type: Web Page
title: Add icons to external links | Docs
description: Learn how to install a rehype plugin to add icons to external links in
  your Markdown files.
resource: https://docs.astro.build/en/recipes/external-links
timestamp: '2026-07-07T10:59:34.007706+00:00'
---

# Add icons to external links

Using a rehype plugin, you can identify and modify links in your Markdown files that point to external sites. This example adds icons to the end of each external link, so that visitors will know they are leaving your site.

## Prerequisites

Section titled “Prerequisites”- An Astro project using Markdown for content pages.

## Recipe

Section titled “Recipe”- 
Install both the `rehype-external-links`plugin and`@astrojs/markdown-remark`.
- 
Configure the plugin in your `astro.config.mjs`file.Import `unified()`and define it as the Markdown processor to support remark plugins. Then, pass to`rehypePlugins`an array containing your imported`rehypeExternalLinks`plugin and an options object with a`content`property. Set this property’s`type`to`text`if you want to add plain text to the end of the link. To add HTML to the end of the link instead, set the property`type`to`raw`.The value of the `content`property is not represented in the accessibility tree. As such, it’s best to make clear that the link is external in the surrounding content, rather than relying on the icon alone.

# Citations

1. Source page: https://docs.astro.build/en/recipes/external-links
