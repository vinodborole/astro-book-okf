---
type: Web Page
title: Data fetching | Docs
description: Learn how to fetch remote data with Astro using the fetch API.
resource: https://docs.astro.build/en/guides/data-fetching
timestamp: '2026-07-07T10:59:34.007706+00:00'
---

# Data fetching

`.astro` files can fetch remote data to help you generate your pages.

`fetch()` in Astro

Section titled “fetch() in Astro”All Astro components have access to the global `fetch()` function in their component script to make HTTP requests to APIs using the full URL (e.g. `https://example.com/api`).
Additionally, you can construct a URL to your project’s pages and endpoints that are rendered on demand on the server using `new URL("/api", Astro.url)`.

This fetch call will be executed at build time, and the data will be available to the component template for generating dynamic HTML. If SSR mode is enabled, any fetch calls will be executed at runtime.

💡 Take advantage of **top-level  await** inside of your Astro component script.

💡 Pass fetched data to both Astro and framework components, as props.

Remember, all data in Astro components is fetched when a component is rendered.

Your deployed Astro site will fetch data **once, at build time**. In dev, you will see data fetches on component refreshes. If you need to re-fetch data multiple times client-side, use a framework component or a client-side script in an Astro component.

`fetch()` in Framework Components

Section titled “fetch() in Framework Components”The `fetch()` function is also globally available to any framework components:

## GraphQL queries

Section titled “GraphQL queries”Astro can also use `fetch()` to query a GraphQL server with any valid GraphQL query.

## Fetch from a Headless CMS

Section titled “Fetch from a Headless CMS”Astro components can fetch data from your favorite CMS and then render it as your page content. Using dynamic routes, components can even generate pages based on your CMS content.

See our CMS Guides for full details on integrating Astro with headless CMSes including Storyblok, Contentful, and WordPress.

# Citations

1. Source page: https://docs.astro.build/en/guides/data-fetching
