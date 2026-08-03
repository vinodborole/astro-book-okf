---
type: Web Page
title: On-demand rendering | Docs
description: Generate server-rendered pages and routes on demand with an adapter.
resource: https://docs.astro.build/en/guides/on-demand-rendering
timestamp: '2026-08-03T09:35:37.104348+00:00'
---

# On-demand rendering

Your Astro project code must be **rendered** to HTML in order to be displayed on the web.

By default, Astro pages, routes, and API endpoints will be pre-rendered at build time as static pages. However, you can choose to render some or all of your routes on demand by a server when a route is requested.

On-demand rendered pages and routes are generated per visit, and can be customized for each viewer. For example, a page rendered on demand can show a logged-in user their account information or display freshly updated data without requiring a full-site rebuild.

On-demand rendering on the server at request time is also known as **server-side rendering (SSR)**.

## Server adapters

[Section titled “Server adapters”](#server-adapters)

To render any page on demand, you need to add an **adapter**. Each adapter allows Astro to output a script that runs your project on a specific **runtime**: the environment that runs code on the server to generate pages when they are requested (e.g. Netlify, Cloudflare).

You may also wish to add an adapter even if your site is entirely static and you are not rendering any pages on demand. For example, the [Netlify adapter](/en/guides/integrations-guide/netlify/) enables Netlify’s Image CDN, and [server islands](/en/guides/server-islands/) require an adapter installed to use `server:defer` on a component.

### Adapters

Astro maintains official adapters for [Node.js](https://nodejs.org/), [Netlify](https://www.netlify.com/), [Vercel](https://vercel.com/), and [Cloudflare](https://www.cloudflare.com/). You can find both [official and community adapters in our integrations directory](https://astro.build/integrations/?search=&categories%5B%5D=adapters). Choose the one that corresponds to your [deployment environment](/en/guides/deploy/).

### Add an Adapter

[Section titled “Add an Adapter”](#add-an-adapter)

You can add any of the [official adapter integrations maintained by Astro](/en/guides/integrations/#official-integrations) with the following `astro add` command. This will install the adapter and make the appropriate changes to your `astro.config.mjs` file in one step.

For example, to install the Netlify adapter, run:

You can also [add an adapter manually by installing the NPM package](/en/guides/integrations/#installing-an-npm-package) (e.g. `@astrojs/netlify`) and updating `astro.config.mjs` yourself.

Note that different adapters may have different configuration settings. Read each adapter’s documentation, and apply any necessary config options to your chosen adapter in `astro.config.mjs`

## Enabling on-demand rendering

[Section titled “Enabling on-demand rendering”](#enabling-on-demand-rendering)

**By default, your entire Astro site will be prerendered**, and static HTML pages will be sent to the browser. However, you may opt out of prerendering on any routes that require server rendering, for example, a page that checks for cookies and displays personalized content.

First, [add an adapter integration](#add-an-adapter) for your server runtime to enable on-demand server rendering in your Astro project.

Then, add `export const prerender = false` at the top of the individual page or endpoint you want to render on demand. The rest of your site will remain a static site:

The following example shows opting out of prerendering in order to display a random number each time the endpoint is hit:

### `'server'` mode

[Section titled “'server' mode”](#server-mode)

For a **highly dynamic app**, after adding an adapter, you can [set your build output configuration to `output: 'server'`](/en/reference/configuration-reference/#output) to **server-render all your pages by default**. This is the equivalent of opting out of prerendering on every page.

Then, if needed, you can choose to prerender any individual pages that do not require a server to execute, such as a privacy policy or about page.

Add `export const prerender = true` to any page or route to prerender a static page or endpoint:

Start with the default `'static'` mode until you are sure that **most or all** of your pages will be rendered on demand! This ensures that your site is as performant as possible, not relying on a server function to render static content.

The `'server'` output mode does not bring any additional functionality. It only switches the default rendering behavior.

[in the configuration reference.](/en/reference/configuration-reference/#output)

`output` setting
## On-demand rendering features

[Section titled “On-demand rendering features”](#on-demand-rendering-features)

### HTML streaming

[Section titled “HTML streaming”](#html-streaming)

With HTML streaming, a document is broken up into chunks, sent over the network in order, and rendered on the page in that order. Astro uses HTML streaming in on-demand rendering to send each component to the browser as it renders them. This makes sure the user sees your HTML as fast as possible, although network conditions can cause large documents to be downloaded slowly, and waiting for data fetches can block page rendering.

**Related recipe:**

[Using streaming to improve page performance](/en/recipes/streaming-improve-page-performance/)

Features that modify the [Response headers](https://developer.mozilla.org/en-US/docs/Glossary/Response_header) are only available at the **page level**. (You can’t use them inside of components, including layout components.) By the time Astro runs your component code, it has already sent the Response headers and they cannot be modified.

### Cookies

[Section titled “Cookies”](#cookies)

A page or API endpoint rendered on demand can check, set, get, and delete cookies.

The example below updates the value of a cookie for a page view counter:

See more details about [`Astro.cookies` and the `AstroCookie` type](/en/reference/api-reference/#cookies) in the API reference.

### `Response`

[Section titled “Response”](#response)

[`Astro.response`](/en/reference/api-reference/#response) is a standard [`ResponseInit`](https://developer.mozilla.org/en-US/docs/Web/API/Response/Response#options) object. It can be used to set the response status and headers.

The example below sets a response status and status text for a product page when the product does not exist:

#### `Astro.response.headers`

[Section titled “Astro.response.headers”](#astroresponseheaders)

You can set headers using the `Astro.response.headers` object:

#### Return a `Response` object

[Section titled “Return a Response object”](#return-a-response-object)

You can also return a [Response](https://developer.mozilla.org/en-US/docs/Web/API/Response) object directly from any page using on-demand rendering either manually or with [`Astro.redirect`](/en/reference/api-reference/#redirect).

The example below looks up an ID in the database on a dynamic page and either it returns a 404 if the product does not exist, or it redirects the user to another page if the product is no longer available, or it displays the product:

### `Request`

[Section titled “Request”](#request)

`Astro.request` is a standard [Request](https://developer.mozilla.org/en-US/docs/Web/API/Request) object. It can be used to get the `url`, `headers`, `method`, and even the body of the request.

You can access additional information from this object for pages that are not statically generated.

#### `Astro.request.headers`

[Section titled “Astro.request.headers”](#astrorequestheaders)

The headers for the request are available on `Astro.request.headers`. This works like the browser’s [`Request.headers`](https://developer.mozilla.org/en-US/docs/Web/API/Request/headers). It is a [Headers](https://developer.mozilla.org/en-US/docs/Web/API/Headers) object where you can retrieve headers such as the cookie.

#### `Astro.request.method`

[Section titled “Astro.request.method”](#astrorequestmethod)

The HTTP method used in the request is available as `Astro.request.method`. This works like the browser’s [`Request.method`](https://developer.mozilla.org/en-US/docs/Web/API/Request/method). It returns the string representation of the HTTP method used in the request.

See more details about [`Astro.request`](/en/reference/api-reference/#request) in the API reference.

### Server Endpoints

[Section titled “Server Endpoints”](#server-endpoints)

A server endpoint, also known as an **API route**, is a special function exported from a `.js` or `.ts` file within the `src/pages/` folder. A powerful feature of server-side rendering on demand, API routes are able to securely execute code on the server.

The function takes an [endpoint context](/en/reference/api-reference/) and returns a [Response](https://developer.mozilla.org/en-US/docs/Web/API/Response).

To learn more, see our [Endpoints Guide](/en/guides/endpoints/#server-endpoints-api-routes).

[Contribute](/en/contribute/)

[Community](https://astro.build/chat)

[Sponsor](https://opencollective.com/astrodotbuild)

# Citations

1. Source page: https://docs.astro.build/en/guides/on-demand-rendering
