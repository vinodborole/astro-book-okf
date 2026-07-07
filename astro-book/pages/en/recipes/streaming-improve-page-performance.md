---
type: Web Page
title: Using streaming to improve page performance | Docs
description: Learn how to use streaming to improve page performance.
resource: https://docs.astro.build/en/recipes/streaming-improve-page-performance
timestamp: '2026-07-07T10:59:34.007706+00:00'
---

# Using streaming to improve page performance

Astro’s SSR uses HTML streaming to send each component to the browser when available for faster page loading. To improve your page’s performance even further, you can build your components strategically to optimize their loading by avoiding blocking data fetches.

The following refactoring example demonstrates how to improve page performance by moving fetch calls to other components, moving them out of a component where they block page rendering.

The following page `await`s some data in its frontmatter. Astro will wait for all of the `fetch` calls to resolve before sending any HTML to the browser.

Moving the `await` calls into smaller components allows you to take advantage of Astro’s streaming. Using the following components to perform the data fetches, Astro can render some HTML first, such as the title, and then the paragraphs when the data is ready.

The Astro page below using these components can render parts of the page sooner. The `<head>`, `<body>`, and `<h2>` tags are no longer blocked by data fetches. The server will then fetch data for `RandomName` and `RandomFact` in parallel and stream the resulting HTML to the browser.

#### Including Promises directly

Section titled “Including Promises directly”You can also include promises directly in the template. Instead of blocking the entire component, it will resolve the promise in parallel and only block the markup that comes after it.

In this example, `A name` will render while `personPromise` and `factPromise` are loading.
Once `personPromise` has resolved, `A fact` will appear and `factPromise` will render when it’s finished loading.

# Citations

1. Source page: https://docs.astro.build/en/recipes/streaming-improve-page-performance
