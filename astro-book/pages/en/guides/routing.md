---
type: Web Page
title: Routing | Docs
description: An intro to routing with Astro.
resource: https://docs.astro.build/en/guides/routing
timestamp: '2026-08-03T09:35:37.104348+00:00'
---

# Routing

Astro uses **file-based routing** to generate your build URLs based on the file layout of your project `src/pages/` directory.

## Navigating between pages

[Section titled “Navigating between pages”](#navigating-between-pages)

Astro uses standard HTML [`<a>` elements](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/a) to navigate between routes. There is no framework-specific `<Link>` component provided.

## Static routes

[Section titled “Static routes”](#static-routes)

`.astro` [page components](/en/basics/astro-pages/) as well as Markdown and MDX Files (`.md`, `.mdx`) within the `src/pages/` directory **automatically become pages on your website**. Each page’s route corresponds to its path and filename within the `src/pages/` directory.

There is no separate “routing config” to maintain in an Astro project! When you add a file to the `src/pages/` directory, a new route is automatically created for you. In static builds, you can customize the file output format using the [`build.format`](/en/reference/configuration-reference/#buildformat) configuration option.

## Dynamic routes

[Section titled “Dynamic routes”](#dynamic-routes)

An Astro page file can specify dynamic route parameters in its filename to generate multiple, matching pages. For example, `src/pages/authors/[author].astro` generates a bio page for every author on your blog. `author` becomes a *parameter* that you can access from inside the page.

In Astro’s default static output mode, these pages are generated at build time, and so you must predetermine the list of `author`s that get a corresponding file. In SSR mode, a page will be generated on request for any route that matches.

### Static (SSG) Mode

[Section titled “Static (SSG) Mode”](#static-ssg-mode)

Because all routes must be determined at build time, a dynamic route must export a `getStaticPaths()` that returns an array of objects with a `params` property. Each of these objects will generate a corresponding route.

`[dog].astro` defines the dynamic `dog` parameter in its filename, so the objects returned by `getStaticPaths()` must include `dog` in their `params`. The page can then access this parameter using `Astro.params`.

This will generate three pages: `/dogs/clifford`, `/dogs/rover`, and `/dogs/spot`, each displaying the corresponding dog name.

The filename can include multiple parameters, which must all be included in the `params` objects in `getStaticPaths()`:

This will generate `/en-v1/info` and `/fr-v2/info`.

Parameters can be included in separate parts of the path. For example, the file `src/pages/[lang]/[version]/info.astro` with the same `getStaticPaths()` above will generate the routes `/en/v1/info` and `/fr/v2/info`.

#### Decoding `params`

[Section titled “Decoding params”](#decoding-params)

`params` returned by a `getStaticPaths()` function are not decoded. Use [`decodeURI()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/decodeURI) when you need to decode parameter values.

[.](/en/reference/routing-reference/#getstaticpaths)

`getStaticPaths()`
**Related recipe:**

[Add i18n features](/en/recipes/i18n/)

#### Rest parameters

[Section titled “Rest parameters”](#rest-parameters)

If you need more flexibility in your URL routing, you can use a [rest parameter](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters) (`[...path]`) in your `.astro` filename to match file paths of any depth:

This will generate `/sequences/one/two/three`, `/sequences/four`, and `/sequences`. (Setting the rest parameter to `undefined` allows it to match the top level page.)

Rest parameters can be used with **other named parameters**. For example, GitHub’s file viewer can be represented with the following dynamic route:

In this example, a request for `/withastro/astro/tree/main/docs/public/favicon.svg` would be split into the following named parameters:

#### Example: Dynamic pages at multiple levels

[Section titled “Example: Dynamic pages at multiple levels”](#example-dynamic-pages-at-multiple-levels)

In the following example, a rest parameter (`[...slug]`) and the [`props`](/en/reference/routing-reference/#data-passing-with-props) feature of `getStaticPaths()` generate pages for slugs of different depths.

### On-demand dynamic routes

[Section titled “On-demand dynamic routes”](#on-demand-dynamic-routes)

For [on-demand rendering](/en/guides/on-demand-rendering/) with an adapter, dynamic routes are defined the same way: include `[param]` or `[...path]` brackets in your file names to match arbitrary strings or paths. But because the routes are no longer built ahead of time, the page will be served to any matching route. Since these are not “static” routes, `getStaticPaths` should not be used.

For on-demand rendered routes, only one rest parameter using the spread notation may be used in the file name (e.g. `src/pages/[locale]/[...slug].astro` or `src/pages/[...locale]/[slug].astro`, but not `src/pages/[...locale]/[...slug].astro`).

This page will be served for any value of `resource` and `id`: `resources/users/1`, `resources/colors/blue`, etc.

#### Modifying the `[...slug]` example for SSR

[Section titled “Modifying the \[...slug\] example for SSR”](#modifying-the-slug-example-for-ssr)

Because SSR pages can’t use `getStaticPaths()`, they can’t receive props. The [previous example](#example-dynamic-pages-at-multiple-levels) can be adapted for SSR mode by looking up the value of the `slug` param in an object. If the route is at the root (“/”), the `slug` param will be `undefined`. If the value doesn’t exist in the object, we redirect to a 404 page.

## Redirects

[Section titled “Redirects”](#redirects)

Sometimes you will need to redirect your readers to a new page, either permanently because your site structure has changed or in response to an action such as logging in to an authenticated route.

You can define rules to [redirect users to permanently-moved pages](#configured-redirects) in your Astro config. Or, [redirect users dynamically](#dynamic-redirects) as they use your site.

### Configured Redirects

[Section titled “Configured Redirects”](#configured-redirects)

	**Added in:**
	`astro@2.9.0`
	
	

You can specify a mapping of permanent redirects in your Astro config with the [`redirects`](/en/reference/configuration-reference/#redirects) value.

For internal redirects, this is a mapping of an old route path to the new route. As of Astro v5.2.0, it is also possible to redirect to external URLs that start with `http` or `https` and [can be parsed](https://developer.mozilla.org/en-US/docs/Web/API/URL/canParse_static):

These redirects follow [the same priority rules as file-based routes](#route-priority-order) and will always take lower precedence than an existing page file of the same name in your project. For example, `/old-page` will not redirect to `/new-page` if your project contains the file `src/pages/old-page.astro`.

Dynamic routes are allowed as long as both the new and old routes contain the same parameters, for example:

Using SSR or a static adapter, you can also provide an object as the value, allowing you to specify the `status` code in addition to the new `destination`:

When running `astro build`, Astro will output HTML files with the [meta refresh](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/meta#examples) tag by default. Supported adapters will instead write out the host’s configuration file with the redirects.

The status code is `301` by default. If building to HTML files the status code is not used by the server.

### Dynamic redirects

[Section titled “Dynamic redirects”](#dynamic-redirects)

On the `Astro` global, the `Astro.redirect` method allows you to redirect to another page dynamically. You might do this after checking if the user is logged in by getting their session from a cookie.

Because Astro uses [HTML streaming](/en/guides/on-demand-rendering/#html-streaming) in on-demand rendering, redirects must be done at the page level, not inside child components.

## Rewrites

[Section titled “Rewrites”](#rewrites)

	**Added in:**
	`astro@4.13.0`
	
	

A rewrite allows you to serve a different route without redirecting the browser to a different page. The browser will show the original address in the URL bar, but will instead display the content of the URL provided to [`Astro.rewrite()`](/en/reference/api-reference/#rewrite).

For content that has permanently moved, or to direct your user to a different page with a new URL (e.g. a user dashboard after logging in), use a [redirect](#redirects) instead.

Rewrites can be useful for showing the same content at multiple paths (e.g. `/products/shoes/men/` and `/products/men/shoes/`) without needing to maintain two different source files.

Rewrites are also useful for SEO purposes and user experience. They allow you to display content that otherwise would require redirecting your visitor to a different page or would return a 404 status. One common use of rewrites is to show the same localized content for different variants of a language.

The following example uses a rewrite to render the `/es/` version of a page when the `/es-CU/` (Cuban Spanish) URL path is visited. When a visitor navigates to the URL `/es-cu/articles/introduction`, Astro will render the content generated by the file `src/pages/es/articles/introduction.astro`.

Use `context.rewrite()` in your endpoint files to reroute to a different page:

If the URL passed to `Astro.rewrite()` emits a runtime error, Astro will show the overlay error in development and return a 500 status code in production. If the URL does not exist in your project, a 404 status code will be returned.

You can intentionally create a rewrite to render your `/404` page, for example to indicate that a product in your e-commerce shop is no longer available:

You can also conditionally rewrite based on an HTTP response status, for example to display a certain page on your site when visiting a URL that doesn’t exist:

Before displaying the content from the specified rewrite path, the function `Astro.rewrite()` will trigger a new, complete rendering phase. This re-executes any middleware for the new route/request.

[for more information.](/en/reference/api-reference/#rewrite)

`Astro.rewrite()` API reference
## Route Priority Order

[Section titled “Route Priority Order”](#route-priority-order)

It’s possible for multiple defined routes to attempt to build the same URL path. For example, all of these routes could build `/posts/create`:

- ## Directorysrc/pages/
  - […slug].astro
  - ## Directoryposts/
    - create.astro
    - [page].astro
    - [pid].ts
    - […slug].astro

Astro needs to know which route should be used to build the page. To do so, it sorts them according to the following rules in order:

- Astro [reserved routes](#reserved-routes)
- Routes with more path segments will take precedence over less specific routes. In the example above, all routes under `/posts/` take precedence over`/[...slug].astro` at the root.
- Static routes without path parameters will take precedence over dynamic routes. E.g. `/posts/create.astro` takes precedence over all the other routes in the example.
- Dynamic routes using named parameters take precedence over rest parameters. E.g. `/posts/[page].astro` takes precedence over`/posts/[...slug].astro` .
- Pre-rendered dynamic routes take precedence over server dynamic routes.
- Endpoints take precedence over pages.
- File-based routes take precedence over redirects.
- If none of the rules above decide the order, routes are sorted alphabetically based on the default locale of your Node installation.

Given the example above, here are a few examples of how the rules will match a requested URL to the route used to build the HTML:

- `pages/posts/create.astro` - Will build only`/posts/create`
- `pages/posts/[pid].ts` - Will build`/posts/abc` ,`/posts/xyz` , etc. But not`/posts/create`
- `pages/posts/[page].astro` - Will build`/posts/1` ,`/posts/2` , etc. But not`/posts/create` ,`/posts/abc` nor`/posts/xyz`
- `pages/posts/[...slug].astro` - Will build`/posts/1/2` ,`/posts/a/b/c` , etc. But not`/posts/create` ,`/posts/1` ,`/posts/abc` , etc.
- `pages/[...slug].astro` - Will build`/abc` ,`/xyz` ,`/abc/xyz` , etc. But not`/posts/create` ,`/posts/1` ,`/posts/abc` , etc.

### Reserved routes

[Section titled “Reserved routes”](#reserved-routes)

Internal routes take priority over any user-defined or integration-defined routes as they are required for Astro features to work. The following are Astro’s reserved routes:

- `_astro/` : Serves all of the static assets to the client, including CSS documents, bundled client scripts, optimized images, and any Vite assets.
- `_server_islands/` : Serves the dynamic components deferred into a[server island](/en/guides/server-islands/) .
- `_actions/` : Serves any defined[actions](/en/guides/actions/) .

## Pagination

[Section titled “Pagination”](#pagination)

Astro supports built-in pagination for large collections of data that need to be split into multiple pages. Astro will generate common pagination properties, including previous/next page URLs, total number of pages, and more.

Paginated route names should use the same `[bracket]` syntax as a standard dynamic route. For instance, the file name `/astronauts/[page].astro` will generate routes for `/astronauts/1`, `/astronauts/2`, etc, where `[page]` is the generated page number.

You can use the `paginate()` function to generate these pages for an array of values like so:

This generates the following pages, with 2 items to a page:

- `/astronauts/1` - Page 1: Displays “Neil Armstrong” and “Buzz Aldrin”
- `/astronauts/2` - Page 2: Displays “Sally Ride” and “John Glenn”

### The `page` prop

[Section titled “The page prop”](#the-page-prop)

When you use the `paginate()` function, each page will be passed its data via a `page` prop. The `page` prop has many useful properties that you can use to build pages and links between them:

The following example displays current information for the page along with links to navigate between pages:

[the pagination](/en/reference/routing-reference/#the-pagination-page-prop).

`page` prop
### Nested Pagination

[Section titled “Nested Pagination”](#nested-pagination)

A more advanced use-case for pagination is **nested pagination.** This is when pagination is combined with other dynamic route params. You can use nested pagination to group your paginated collection by some property or tag.

For example, if you want to group your paginated Markdown posts by some tag, you would use nested pagination by creating a `/src/pages/[tag]/[page].astro` page that would match the following URLs:

- `/red/1` (tag=red)
- `/red/2` (tag=red)
- `/blue/1` (tag=blue)
- `/green/1` (tag=green)

Nested pagination works by returning an array of `paginate()` results from `getStaticPaths()`, one for each grouping.

In the following example, we will implement nested pagination to build the URLs listed above:

## Excluding pages

[Section titled “Excluding pages”](#excluding-pages)

You can exclude pages or directories within `src/pages` from being built by prefixing their names with an underscore (`_`). Files with the `_` prefix won’t be recognized by the router and won’t be placed into the `dist/` directory.

You can use this to temporarily disable pages, and also to put tests, utilities, and components in the same folder as their related pages.

In this example, only `src/pages/index.astro` and `src/pages/projects/project1.md` will be built as page routes and HTML files.

- ## Directorysrc/pages/
  - ## Directory_hidden-directory/
    - page1.md
    - page2.md
  - _hidden-page.astro
  - **index.astro**
  - ## Directoryprojects/
    - _SomeComponent.astro
    - _utils.js
    - **project1.md**

## Advanced routing

[Section titled “Advanced routing”](#advanced-routing)

	**Added in:**
	`astro@7.0.0`
	
	

By default, Astro handles every request with a built-in pipeline that runs the handlers in a fixed order: trailing-slash normalization, redirects, sessions, actions, user middleware, page rendering, i18n, and caching. This pipeline is designed to cover the most common use cases for routing and request handling, but it may not fit every project’s needs.

Astro’s advanced routing allows you to replace this pipeline with your own. You can choose which built-in features to use and where to use them. You can also add your own custom logic anywhere in the pipeline. This gives you full control over how Astro handles incoming requests.

### Creating a custom entrypoint

[Section titled “Creating a custom entrypoint”](#creating-a-custom-entrypoint)

When the default pipeline does not fit your needs, you can override it by creating a `src/fetch.ts` file that default-exports an object with a `fetch()` method. This method receives a standard [Request](https://developer.mozilla.org/en-US/docs/Web/API/Request) and must return a [Response](https://developer.mozilla.org/en-US/docs/Web/API/Response).

Astro supports several file formats for its advanced routing entrypoint: `.ts`, `.js`, `.mjs`, and `.mts`. We recommend using `.js` in most cases or `.ts` if you need TypeScript support.

### Changing the entrypoint filename

[Section titled “Changing the entrypoint filename”](#changing-the-entrypoint-filename)

By default, Astro looks for `src/fetch.ts` as the advanced routing entrypoint. You can change this by setting the [`fetchFile`](/en/reference/configuration-reference/#fetchfile) option in your Astro config file.

The following example tells Astro to look for `src/handler.ts` instead of `src/fetch.ts`:

Set `fetchFile` to `null` to disable the entrypoint entirely. This is useful if you already have a `src/fetch.ts` file used for other purposes:

### Adding custom logic

[Section titled “Adding custom logic”](#adding-custom-logic)

The main benefit of advanced routing is the ability to insert custom logic into the request pipeline. You can run code before Astro touches the request, between pipeline stages, or after the response is produced.

You can do this in two ways:

- Use the [`astro()` handler](/en/reference/modules/astro-fetch/#astro) to run the full built-in pipeline, and add logic before or after it.
- Compose individual handlers from [`astro/fetch`](/en/reference/modules/astro-fetch/) or[`astro/hono`](/en/reference/modules/astro-hono/) for more control over execution order.

#### Running the full pipeline with `astro()`

[Section titled “Running the full pipeline with astro()”](#running-the-full-pipeline-with-astro)

Use [`astro()`](/en/reference/modules/astro-fetch/#astro) when you want to keep Astro’s built-in routing behavior, but need custom logic around it. This approach preserves the default pipeline order and lets you add pre-processing and post-processing in one place. For many use cases, such as adding auth guards, request logging, and custom headers, `astro()` is all you need.

The following example checks if a user can access a dashboard before running the Astro pipeline, and adds a custom header to the response once Astro has finished running:

#### Composing individual handlers

[Section titled “Composing individual handlers”](#composing-individual-handlers)

When you need more control over the pipeline execution order, or want to omit certain features, you can compose individual handler functions from [`astro/fetch`](/en/reference/modules/astro-fetch/). Each handler operates on a [`FetchState` object](/en/reference/modules/astro-fetch/#fetchstate) that tracks per-request data, such as the matched route, cookies, and session. You can call handlers in any order and insert custom logic between stages.

The following example runs only the handlers used in the project and adds custom logic after actions and before page rendering:

### Using with Hono

[Section titled “Using with Hono”](#using-with-hono)

Astro also provides Hono-compatible wrappers for all handler functions via [`astro/hono`](/en/reference/modules/astro-hono/). If you prefer to use [Hono](https://hono.dev/) as your routing framework, you can export a Hono app from `src/fetch.ts`:

[Contribute](/en/contribute/)

[Community](https://astro.build/chat)

[Sponsor](https://opencollective.com/astrodotbuild)

# Citations

1. Source page: https://docs.astro.build/en/guides/routing
