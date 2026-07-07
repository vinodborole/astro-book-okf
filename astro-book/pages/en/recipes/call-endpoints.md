---
type: Web Page
title: Call endpoints from the server | Docs
description: Learn how to call endpoints from the server in Astro.
resource: https://docs.astro.build/en/recipes/call-endpoints
timestamp: '2026-07-07T10:59:34.007706+00:00'
---

# Call endpoints from the server

Endpoints can be used to serve many kinds of data. This recipe calls a server endpoint from a page’s component script to display a greeting, without requiring an additional fetch request.

## Prerequisites

Section titled “Prerequisites”- A project with SSR (output: ‘server’) enabled

## Recipe

Section titled “Recipe”- 
Create an endpoint in a new file `src/pages/api/hello.ts`that returns some data:
- 
On any Astro page, import the `GET()`method from the endpoint. Call it with the`Astro`global to provide the request context, and use the response on the page:

# Citations

1. Source page: https://docs.astro.build/en/recipes/call-endpoints
