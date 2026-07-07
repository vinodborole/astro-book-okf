---
type: Web Page
title: Route caching | Docs
description: An intro to caching with Astro.
resource: https://docs.astro.build/en/guides/caching
timestamp: '2026-07-07T10:59:34.007706+00:00'
---

# Route caching

	**Added in:**
	`astro@7.0.0`
	New
	

Astro provides a platform-agnostic API for caching responses from on-demand rendered pages and endpoints. Cache directives set in your routes are translated into the appropriate headers or runtime behavior depending on your configured cache provider.

Route caching builds on standard HTTP caching semantics, including `max-age` and `stale-while-revalidate`, with support for tag-based and path-based invalidation, config-level route rules, and pluggable cache providers that adapters can set automatically.

## Configure caching

Section titled “Configure caching”Route caching requires a cache provider to determine how caching is implemented at runtime. A built-in in-memory provider is available, and custom providers can be implemented for advanced use cases and specific runtimes.

To enable this feature, set a cache provider in your Astro config:

You can then use `Astro.cache` in your `.astro` pages (or `context.cache` for API routes and middleware) to control caching per request. Cache defaults for groups of routes can also be defined declaratively in your config using `routeRules`.

If you deploy to Netlify, Vercel, or Cloudflare, you can use their respective adapters’ experimental CDN cache provider instead of the in-memory provider.

## Adapter cache providers

Section titled “Adapter cache providers”Astro’s first-party adapters for Netlify, Vercel, and Cloudflare each provide an experimental CDN cache provider that maps cache directives to the platform’s native cache headers and invalidation API. Rather than storing responses in memory, these push your caching directives to the host’s edge network, and cache hits are served straight from the CDN without invoking your server function.

During the experimental phase these providers need to be manually enabled, as shown below. In a future release, they will be enabled automatically by their adapters.

Each provider automatically tags cached responses with the request path, so `cache.invalidate({ path })` works on platforms that only support tag-based purges.

### Netlify

Section titled “Netlify”
	**Added in:**
	`@astrojs/netlify@8.0.0`
	
	

Import `cacheNetlify()` from `@astrojs/netlify/cache` and set it as your cache provider:

The provider sets `Netlify-CDN-Cache-Control` and `Netlify-Cache-Tag` headers. Cached responses use Netlify’s durable cache so they are shared across all edge nodes, reducing function invocations. Both tag-based and path-based invalidation are supported.

### Vercel

Section titled “Vercel”
	**Added in:**
	`@astrojs/vercel@11.0.0`
	New
	

Import `cacheVercel()` from `@astrojs/vercel/cache` and set it as your cache provider:

The provider sets `Vercel-CDN-Cache-Control` and `Vercel-Cache-Tag` headers. Both tag-based and path-based invalidation are supported. Tag invalidation is a soft invalidation: cached responses are marked as stale and revalidated in the background using stale-while-revalidate.

### Cloudflare

Section titled “Cloudflare”
	**Added in:**
	`@astrojs/cloudflare@14.0.0`
	
	

Import `cacheCloudflare()` from `@astrojs/cloudflare/cache` and set it as your cache provider:

The provider sets `Cloudflare-CDN-Cache-Control` and `Cache-Tag` headers. Both tag-based and path-based invalidation are supported.

The adapter enables the Cloudflare Workers Cache with default settings when a Cloudflare cache provider is used. You can change the configuration if needed, for example if you want to preserve the cache when you deploy a new version of the site.

## Interacting with the cache

Section titled “Interacting with the cache”The `cache` object provides methods for setting cache options, invalidating entries, and checking the current cache state. This object is available in your `.astro` pages as `Astro.cache`, and in API routes and middleware as `context.cache`.

### Checking if caching is enabled

Section titled “Checking if caching is enabled”When caching is not configured, `cache.set()`, `cache.tags`, and `cache.options` log a warning, and `cache.invalidate()` throws an error. To avoid this, wrap your caching logic in a conditional check using `cache.enabled`. Its value is always `false` when no provider is configured or in development mode.

### Setting cache options

Section titled “Setting cache options”Call `cache.set()` with an options object to enable caching for the current response.

The following example caches a page for 2 minutes, serves stale content for 1 minute while revalidating, and tags the response for targeted invalidation:

In API routes and middleware, use `context.cache`:

### Opting out of caching

Section titled “Opting out of caching”Call `cache.set()` with `false` to explicitly opt a request out of caching. This is useful when a matched route rule would otherwise cache the response:

### Reading cache state

Section titled “Reading cache state”You can access the current accumulated cache options via `cache.options`. This is useful for debugging or when you want to conditionally modify caching based on the current state:

### Invalidating cache entries

Section titled “Invalidating cache entries”You can purge cached entries by tag or path using `cache.invalidate()`. This is useful for programmatically clearing cached content when it becomes stale, such as after a content update or user action.

The following example creates an API route that invalidates by tag and by path:

Tag-based invalidation removes all cached entries whose tags include any of the provided tags. Path-based invalidation is exact-match only (no glob or wildcard patterns).

## Merge behavior

Section titled “Merge behavior”Multiple calls to `cache.set()` within a single request are merged according to the following rules:

- **Scalar values**(- `maxAge`,- `swr`,- `etag`): last-write-wins
- `lastModified`
- `tags`

Middleware, layouts, content loaders, and page code can each contribute cache directives independently.

## Dev mode behavior

Section titled “Dev mode behavior”In dev mode, the cache API is available so that route code does not need conditional checks, but no actual caching occurs. `cache.enabled` is `false`, and `cache.set()` and `cache.invalidate()` are no-ops. To test your caching locally, build then preview your site.

## Route rules

Section titled “Route rules”Route rules allow you to define caching behavior for groups of routes declaratively in your config. This is useful for applying caching to large groups of routes at once.

The following example caches all API routes with stale-while-revalidate, product pages with a 1-hour freshness window, and blog posts for 5 minutes:

The following route patterns are supported:

- **Static paths**:- `/about`,- `/api/health`
- **Dynamic parameters**:- `/products/[id]`,- `/blog/[slug]`
- **Rest parameters**:- `/docs/[...path]`

Patterns use the same syntax, matching, and priority rules as Astro’s file-based routing, so more specific patterns take precedence. Glob wildcards such as `*` are not supported; use a `[...rest]` parameter to match a group of routes (for example, `/api/[...path]` to match everything under `/api`).

Per-route `cache.set()` calls merge with config-level route rules. Route code can override or extend the defaults set in config. For example, a route rule might set a default `maxAge` for all product pages, but individual pages can call `cache.set()` to customize or disable caching as needed.

# Citations

1. Source page: https://docs.astro.build/en/guides/caching
