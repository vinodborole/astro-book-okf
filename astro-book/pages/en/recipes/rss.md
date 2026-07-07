---
type: Web Page
title: Add an RSS feed | Docs
description: Add an RSS feed to your Astro site to let users subscribe to your content.
resource: https://docs.astro.build/en/recipes/rss
timestamp: '2026-07-07T10:59:34.007706+00:00'
---

# Add an RSS feed

Astro supports fast, automatic RSS feed generation for blogs and other content websites. RSS feeds provide an easy way for users to subscribe to your content.

## Setting up `@astrojs/rss`

Section titled “Setting up @astrojs/rss”The package `@astrojs/rss` provides helpers for generating RSS feeds using API endpoints. This unlocks both static builds *and* on-demand generation when using an SSR adapter.

- 
Install `@astrojs/rss`using your preferred package manager:Ensure you’ve configured a `site`in your project’s`astro.config`. This will be used to generate links to your RSS articles.
- 
Create a file in `src/pages/`with a name of your choice and the extension`.xml.js`to be used as the output URL for your feed. Some common RSS feed URL names are`feed.xml`or`rss.xml`.The example file below `src/pages/rss.xml.js`will create an RSS feed at`site/rss.xml`.
- 
Import the `rss()`helper from the`@astrojs/rss`package into your`.xml.js`file and export a function that returns it using the following parameters:

`@astrojs/rss` README for the full configuration reference.
## Generating `items`

Section titled “Generating items”The `items` field accepts a list of RSS feed objects, which can be generated from content collections entries using `getCollection()` or from your page files using `pagesGlobToRssItems()`.

The RSS feed standard format includes metadata for each published item, including values such as:

- `title`: The title of the entry. Optional only if a- `description`is set. Otherwise, required.
- `description`: A short excerpt from or describing the entry. Optional only if a- `title`is set. Otherwise, required.
- `link`: A URL to the original source of the entry. (optional)
- `pubDate`: The date of publication of the entry. (optional)
- `content`: The full content of your post. (optional)

`items` configuration reference for a complete list of options.
### Using content collections

Section titled “Using content collections”To create an RSS feed of pages managed in content collections, use the `getCollection()` function to retrieve the data required for your `items` array. You will need to specify the values for each desired property (e.g. `title`, `description`) from the returned data.

Optional: replace your existing blog collection schema to enforce the expected RSS properties.

To ensure that every blog entry produces a valid RSS feed item, you can optionally import and apply `rssSchema` instead of defining each individual property of your schema.

### Using glob imports

Section titled “Using glob imports”
	**Added in:**
	`@astrojs/rss@2.1.0`
	
	

To create an RSS feed from documents in `src/pages/`, use the `pagesGlobToRssItems()` helper. This accepts an `import.meta.glob` result and outputs an array of valid RSS feed items (see more about writing glob patterns for specifying which pages to include).

This function assumes, but does not verify, that all necessary feed properties are present in each document’s frontmatter. If you encounter errors, verify each page frontmatter manually.

In versions of `@astrojs/rss` before v2.1.0, pass your glob result straight to `items` without the `pagesGlobToRssItems()` wrapper:

This method is deprecated for all versions of Astro since v2.1.0, and cannot be used on modern projects.

### Including full post content

Section titled “Including full post content”
	**Added in:**
	`astro@1.6.14`
	
	

Set the `content` key on `rss.items` to provide the full content of a post as HTML. This allows `@astrojs/rss` to make the full Markdown text of your post available to RSS feed readers. Images and links with full URL paths are also supported. However, images and internal links to other pages using relative paths are not.

When rendering full post content, you will have to consider images, relative links, styles, scripts, and other elements beyond standard Markdown text that you may have in your posts. You may need to include additional logic in your `src/pages/rss.xml.js` endpoint to account for these, or to remove elements that are unnecessary for an RSS feed (e.g. those that are used only for styling or interaction on your website).

You can see one specific community implementation that addresses some of these concerns for an example of how to proceed.

A package like `sanitize-html` will make sure that your content is properly sanitized, escaped, and encoded. In the process, such a package might also remove some harmless elements and attributes, so make sure to verify the output and configure the package according to your needs.

When using content collections, render the post `body` using a standard Markdown parser like `markdown-it` and sanitize the result, including any extra tags (e.g. `<img>`) needed to render your content:

When using glob imports with Markdown, you may use the `compiledContent()` helper to retrieve the rendered HTML for sanitization. Note: this feature is **not** supported for MDX files.

## Removing trailing slashes

Section titled “Removing trailing slashes”Astro’s RSS feed produces links with a trailing slash by default, no matter what value you have configured for `trailingSlash`. This means that your RSS links may not match your post URLs exactly.

If you have set `trailingSlash: "never"` on your `astro.config.mjs`, set `trailingSlash: false` in the `rss()` helper so that your feed matches your project configuration.

## Adding a stylesheet

Section titled “Adding a stylesheet”Style your RSS feed for a more pleasant user experience when viewing the file in your browser.

Use the `rss` function’s `stylesheet` option to specify an absolute path to your stylesheet.

If you’d prefer not to create your own stylesheet, you may use a premade stylesheet such as the Pretty Feed v3 default stylesheet. Download the stylesheet from GitHub and save into your project’s `public/` directory.

## Enabling RSS feed auto-discovery

Section titled “Enabling RSS feed auto-discovery”RSS autodiscovery allows browsers and other software to automatically find a site’s RSS feed from the main URL.

To enable, add a `<link>` tag with the following attributes to your site’s `head` element:

With this tag, readers of your blog can enter your site’s base URL into their RSS reader to subscribe to your posts without needing the specific URL of your RSS feed.

## Next Steps

Section titled “Next Steps”After visiting your feed in the browser at `your-domain.com/rss.xml` and confirming that you can see data for each of your posts, you can now promote your feed on your website. Adding the standard RSS icon to your site lets your readers know that they can subscribe to your posts in their own feed reader.

# Citations

1. Source page: https://docs.astro.build/en/recipes/rss
