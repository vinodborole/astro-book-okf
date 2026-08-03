---
type: Web Page
title: Call endpoints from the server | Docs
description: Learn how to call endpoints from the server in Astro.
resource: https://docs.astro.build/en/recipes/call-endpoints
timestamp: '2026-08-03T09:35:37.104348+00:00'
---

# Call endpoints from the server

Endpoints can be used to serve many kinds of data. This recipe calls a server endpoint from a page’s component script to display a greeting, without requiring an additional fetch request.

## Prerequisites

[Section titled “Prerequisites”](#prerequisites)

- A project with [SSR](/en/guides/on-demand-rendering/) (output: ‘server’) enabled

## Recipe

[Section titled “Recipe”](#recipe)

1. 
Create an endpoint in a new file `src/pages/api/hello.ts` that returns some data:
2. 
On any Astro page, import the `GET()` method from the endpoint. Call it with the[`Astro` global](/en/reference/api-reference/) to provide the request context, and use the response on the page:

[Contribute](/en/contribute/)

[Community](https://astro.build/chat)

[Sponsor](https://opencollective.com/astrodotbuild)

# Citations

1. Source page: https://docs.astro.build/en/recipes/call-endpoints
