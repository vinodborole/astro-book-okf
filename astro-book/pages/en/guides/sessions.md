---
type: Web Page
title: Sessions | Docs
description: Share data between requests for on-demand rendered pages.
resource: https://docs.astro.build/en/guides/sessions
timestamp: '2026-07-07T10:59:34.007706+00:00'
---

# Sessions

	**Added in:**
	`astro@5.7.0`
	
	

Sessions are used to share data between requests for on-demand rendered pages.

Unlike `cookies`, sessions are stored on the server, so you can store larger amounts of data without worrying about size limits or security issues. They are useful for storing things like user data, shopping carts, and form state, and they work without any client-side JavaScript:

## Configuring sessions

Section titled “Configuring sessions”Sessions require a storage driver to store the session data. The Node, Cloudflare, and Netlify adapters automatically configure a default driver for you, but other adapters currently require you to specify a driver manually.

See the `session` configuration option for more details on setting a storage driver, and other configurable options.

### Overriding the configuration at runtime

Section titled “Overriding the configuration at runtime”By default, session drivers are configured at build time, and any environment variables used will be inlined into the build. This means you cannot override the configuration at runtime.

When you need a different configuration (e.g. to connect to an external service), define it in a separate file. Then use that file as the driver’s entrypoint.

The following example takes advantage of Unstorage compatibility to configure the Redis driver in its own entrypoint:

- 
Install the `unstorage`package:
- 
Create a file for the driver configuration (e.g. `src/session-driver.ts`) and export a default function that returns the driver instance:
- 
Use this file as the driver’s entrypoint in your Astro configuration: 

## Interacting with session data

Section titled “Interacting with session data”The `session` object allows you to interact with the stored user state (e.g. adding items to a shopping cart) and the session ID (e.g. deleting the session ID cookie when logging out). The object is accessible as `Astro.session` in your Astro components and pages and as `context.session` object in API endpoints, middleware, and actions.

The session is generated automatically when it is first used and can be regenerated at any time with `session.regenerate()` or destroyed with `session.destroy()`.

For many use cases, you will only need to use `session.get()` and `session.set()`.

See the Sessions API reference for more details.

### Astro components and pages

Section titled “Astro components and pages”In `.astro` components and pages, you can access the session object via the global `Astro` object. For example, to display the number of items in a shopping cart:

### API endpoints

Section titled “API endpoints”In API endpoints, the session object is available on the `context` object. For example, to add an item to a shopping cart:

### Actions

Section titled “Actions”In actions, the session object is available on the `context` object. For example, to add an item to a shopping cart:

### Middleware

Section titled “Middleware”Sessions are not supported in edge middleware.

In middleware, the session object is available on the `context` object. For example, to set the last visit time in the session:

## Session data types

Section titled “Session data types”By default session data is untyped, and you can store arbitrary data in any key. Values are serialized and deserialized using devalue, which is the same library used in content collections and actions. This means that supported types are the same, and include strings, numbers, `Date`, `Map`, `Set`, `URL`, arrays, and plain objects.

You can optionally define TypeScript types for your session data by creating a `src/env.d.ts` file and adding a declaration for the `App.SessionData` type:

This will allow you to access the session data with type-checking and auto-completion in your editor:

This is only used for type-checking and does not affect the runtime behavior of the session. Take extra care if you change the type when users have stored data in the session, as this could cause runtime errors.

# Citations

1. Source page: https://docs.astro.build/en/guides/sessions
