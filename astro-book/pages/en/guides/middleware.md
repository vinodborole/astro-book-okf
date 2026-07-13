---
type: Web Page
title: Middleware | Docs
description: Learn how to use middleware in Astro.
resource: https://docs.astro.build/en/guides/middleware
timestamp: '2026-07-13T09:18:12.222139+00:00'
---

# Middleware

**Middleware** allows you to intercept requests and responses and inject behaviors dynamically every time a page or endpoint is about to be rendered. This rendering occurs at build time for all prerendered pages, but occurs when the route is requested for pages rendered on demand, making [additional SSR features like cookies and headers](/en/guides/on-demand-rendering/#on-demand-rendering-features) available.

Middleware also allows you to set and share request-specific information across endpoints and pages by mutating a `locals` object that is available in all Astro components and API endpoints. This object is available even when this middleware runs at build time.

## Basic Usage

[Section titled “Basic Usage”](#basic-usage)

- 
Create `src/middleware.js|ts`(Alternatively, you can create`src/middleware/index.js|ts`.)
- 
Inside this file, export an `onRequest()``context`object`next()`function. This must not be a default export.
- 
Inside any `.astro`file, access response data using`Astro.locals`.

### The `context` object

[Section titled “The context object”](#the-context-object)

The [ context](/en/reference/api-reference/) object includes information to be made available to other middleware, API routes and 

`.astro` routes during the rendering process.This is an optional argument passed to `onRequest()` that may contain the `locals` object as well as any additional properties to be shared during rendering. For example, the `context` object may include cookies used in authentication.

### Storing data in `context.locals`

[Section titled “Storing data in context.locals”](#storing-data-in-contextlocals)

`context.locals` is an object that can be manipulated inside the middleware.

This `locals` object is forwarded across the request handling process and is available as a property to [ APIContext](/en/reference/api-reference/#locals) and 

[. This allows data to be shared between middlewares, API routes, and](/en/reference/api-reference/#locals)

`AstroGlobal``.astro` pages. This is useful for storing request-specific data, such as user data, across the rendering step.[Integrations](/en/guides/integrations/) may set properties and provide functionality through the `locals` object. If you are using an integration, check its documentation to ensure you are not overriding any of its properties or doing unnecessary work.

You can store any type of data inside `locals`: strings, numbers, and even complex data types such as functions and maps.

Then you can use this information inside any `.astro` file with `Astro.locals`.

`locals` is an object that lives and dies within a single Astro route; when your route page is rendered, `locals` won’t exist anymore and a new one will be created. Information that needs to persist across multiple page requests must be stored elsewhere.

The value of `locals` cannot be overridden at run time. Doing so would risk wiping out all the information stored by the user.  Astro performs checks and will throw an error if `locals` are overridden.

## Example: redacting sensitive information

[Section titled “Example: redacting sensitive information”](#example-redacting-sensitive-information)

The example below uses middleware to replace “PRIVATE INFO” with the word “REDACTED” to allow you to render modified HTML on your page:

## Middleware types

[Section titled “Middleware types”](#middleware-types)

You can import and use the utility function [ defineMiddleware()](/en/reference/modules/astro-middleware/#definemiddleware) to take advantage of type safety:

Instead, if you’re using JsDoc to take advantage of type safety, you can use `MiddlewareHandler`:

To type the information inside `Astro.locals`, which gives you autocompletion inside `.astro` files and middleware code, [extend the global types](/en/guides/typescript/#extending-global-types) by declaring a global namespace in the `env.d.ts` file:

Then, inside the middleware file, you can take advantage of autocompletion and type safety.

## Chaining middleware

[Section titled “Chaining middleware”](#chaining-middleware)

Multiple middlewares can be joined in a specified order using [ sequence()](/en/reference/modules/astro-middleware/#sequence):

This will result in the following console order:

## Rewriting

[Section titled “Rewriting”](#rewriting)

	**Added in:**
	`astro@4.13.0`
	
	

The `APIContext` exposes a method called [ rewrite()](/en/reference/api-reference/#rewrite) which works the same way as 

[Astro.rewrite](/en/guides/routing/#rewrites).

Use `context.rewrite()` inside middleware to display a different page’s content without [redirecting](/en/guides/routing/#dynamic-redirects) your visitor to a new page. This will trigger a new rendering phase, causing any middleware to be re-executed.

You can also pass the `next()` function an optional URL path parameter to rewrite the current `Request` without retriggering a new rendering phase. The location of the rewrite path can be provided as a string, URL, or `Request`:

The `next()` function accepts the same payload as [the  Astro.rewrite() function](/en/reference/api-reference/#rewrite). The location of the rewrite path can be provided as a string, URL, or 

`Request`.When you have multiple middleware functions chained via [sequence()](#chaining-middleware), submitting a path to `next()` will rewrite the `Request` in place and the middleware will not execute again. The next middleware function in the chain will receive the new `Request` with its updated `context`.

Calling `next()` with this signature will create a new `Request` object using the old `ctx.request`. This means that trying to consume `Request.body`, either before or after this rewrite, will throw a runtime error. This error is often raised with [Astro Actions that use HTML forms](/en/guides/actions/#call-actions-from-an-html-form-action). In these cases, we recommend handling rewrites from your Astro templates using `Astro.rewrite()` instead of using middleware.

## Error pages

[Section titled “Error pages”](#error-pages)

Middleware will attempt to run for all on-demand rendered pages, even when a matching route cannot be found. This includes Astro’s default (blank) 404 page and any custom 404 pages. However, it is up to the [adapter](/en/guides/on-demand-rendering/) to decide whether that code runs. Some adapters may serve a platform-specific error page instead.

Middleware will also attempt to run before serving a 500 error page, including a custom 500 page, unless the server error occurred in the execution of the middleware itself. If your middleware does not run successfully, then you will not have access to `Astro.locals` to render your 500 page.

[Contribute](/en/contribute/)

[Community](https://astro.build/chat)

[Sponsor](https://opencollective.com/astrodotbuild)

# Citations

1. Source page: https://docs.astro.build/en/guides/middleware
