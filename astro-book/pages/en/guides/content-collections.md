---
type: Web Page
title: Content collections | Docs
description: Manage your content with type safety.
resource: https://docs.astro.build/en/guides/content-collections
timestamp: '2026-07-13T09:18:12.222139+00:00'
---

# Content collections

	**Added in:**
	`astro@2.0.0`
	
	

**Content collections** are the best way to manage sets of content in any Astro project: blog posts, product descriptions, character profiles, recipes, or any structured content. Collections help to organize and query your documents, enable Intellisense and type checking in your editor, and provide automatic TypeScript type-safety for all of your content.

Astro provides performant, scalable APIs to load, query, and render content from anywhere: stored locally in your project, hosted remotely, or fetched live from frequently-updating sources.

## What are Content Collections?

[Section titled “What are Content Collections?”](#what-are-content-collections)

A content collection is a set of related, structurally identical data. This data can be stored in one or several files locally (e.g. a folder of individual Markdown files of blog posts, a single JSON file of product descriptions) or fetched from remote sources such as a database, CMS, or API endpoint. Each member of the collection is called an entry.

- ## Directorysrc/- …
 
- ## Directory- **newsletter/**the “newsletter” collection- week-1.md a collection entry
- week-2.md a collection entry
- week-3.md a collection entry
 
- ## Directory- **authors/**the “author” collection- authors.json a single file containing all collection entries
 

Collections are defined by the location and shape of its entries and provide a convenient way to query and render your content and associated metadata. You can create a collection any time you have a group of related data or content, stored in the same location, that shares a common structure.

[Two types of content collections](#types-of-collections) are available to allow you to work with data fetched either at build time or at request time. Both build-time collections and live updating collections use:

- A required `loader`to retrieve your content and metadata from wherever it is stored and make it available to your project through content-focused APIs.
- An optional collection `schema`that allows you to define the expected shape of each entry for type safety, autocomplete, and validation in your editor.

Collections stored locally in your project or on your filesystem can use one of Astro’s [provided build-time loaders](#build-time-collection-loaders) to fetch data from Markdown, MDX, Markdoc, YAML, TOML, or JSON files. Point Astro to the location of your content, define your data shape, and you’re good to go with a blog or similarly content-heavy, mostly static site in no time!

With [community-built loaders](https://astro.build/integrations/?search=&categories%5B%5D=loaders) or by building a [custom build-time collection loader](#custom-build-time-loaders) or [live loader](#creating-a-live-loader) yourself, you can fetch remote data from any external source, such as a CMS, database, or headless payment system, either at build time or live on demand.

### Types of collections

[Section titled “Types of collections”](#types-of-collections)

[Build-time content collections](#defining-build-time-content-collections) are updated at build time, and data is saved to a storage layer. This provides excellent performance for most content, but may not be suitable for frequently updating data sources requiring up-to-the-moment data freshness, such as live stock prices.

For the best performance and scalability, use build-time content collections when one or more of these is true:

- **Performance is critical**and you want to prerender data at build time.
- **Your data is relatively static**(e.g., blog posts, documentation, product descriptions).
- **You want to benefit from build-time optimization**and caching.
- **You need to process MDX**or- **perform image optimization**.
- **Your data can be fetched once and reused**across multiple builds.

See [the official Astro blog starter template](https://github.com/withastro/astro/tree/latest/examples/blog) to get up and running quickly with an example of using the [built-in  glob() loader](#the-glob-loader) and 

[defining a schema](#defining-the-collection-schema)for a collection of local Markdown or MDX blog posts.

[Live content collections](#live-content-collections) fetch their data at runtime rather than build time. This allows you to access frequently updated data from CMSs, APIs, databases, or other sources using a unified API, without needing to rebuild your site when the data changes. However, this can come at a performance cost since data is fetched at each request and returned directly with no data store persistence.

Live content collections are designed for data that changes frequently and needs to be up-to-date when a page is requested. Consider using them when one or more of these is true:

- **You need real-time information**(e.g. user-specific data, current stock levels).
- **You want to avoid constant rebuilds**for content that changes often.
- **Your data updates frequently**(e.g. up-to-the-minute product inventory, prices, availability).
- **You need to pass dynamic filters**to your data source based on user input or request parameters.
- **You’re building preview functionality**for a CMS where editors need to see draft content immediately.

Both kinds of collections can exist in the same project, so you can always choose the best type of collection for each individual data source. For example, a build-time collection can manage product descriptions, while a live collection can manage content inventory.

Both types of collections use similar APIs (e.g. `getCollection()` and `getLiveCollection()`), so that working with collections will feel familiar no matter which one you choose, while still ensuring that you always know which type of collection you are working with.

We suggest using build-time content collections whenever possible, and using live collections when your content needs updating in real time and the performance tradeoffs are acceptable. Additionally, live content collections have some limitations compared to build-time collections:

- **No MDX support**: MDX cannot be rendered at runtime
- **No image optimization**: Images cannot be processed at runtime
- **Performance considerations**: Data is fetched on each request (unless cached)
- **No data store persistence**: Data is not saved to the content layer data store

### When to create a collection

[Section titled “When to create a collection”](#when-to-create-a-collection)

Define your data as a collection when:

- You have multiple files or data to organize that share the same overall structure (e.g. a directory of blog posts written in Markdown which all have the same frontmatter properties).
- You have existing content stored remotely, such as in a CMS, and want to take advantage of the collections helper functions instead of using `fetch()`or SDKs.
- You need to fetch (tens of) thousands of related pieces of data at build time, and need a querying and caching method that handles at scale.

Much of the benefit of using collections comes from:

- Defining a common data shape to validate that an individual entry is “correct” or “complete”, avoiding errors in production.
- Content-focused APIs designed to make querying intuitive (e.g. `getCollection()`instead of`import.meta.glob()`) when importing and rendering content on your pages.
- Access to both built-in loaders and access to the low-level [Content Loader API](/en/reference/content-loader-reference/)for retrieving your content. There are additionally several third-party and community-built loaders available, and you can build your own custom loader to fetch data from anywhere.
- Performance and scalability. Build-time content collections data can be cached between builds and is suitable for tens of thousands of content entries.

### When not to create a collection

[Section titled “When not to create a collection”](#when-not-to-create-a-collection)

Collections provide excellent structure, safety, and organization when you have multiple pieces of content that must share the same properties.

Collections may not be your solution if:

- You have only one or a small number of different content pages. Consider [making individual page components](/en/basics/astro-pages/)such as`src/pages/about.astro`with your content directly instead.
- You are displaying files that are not processed by Astro, such as PDFs. Place these static assets in the `public/`directory
- Your data source has its own SDK/client library for imports that is incompatible with or does not offer a content loader, and you prefer to use it directly.

## TypeScript configuration for collections

[Section titled “TypeScript configuration for collections”](#typescript-configuration-for-collections)

Content collections rely on TypeScript to provide Zod validation, Intellisense, and type checking in your editor. By default, Astro configures a [ strict TypeScript template](/en/guides/typescript/#tsconfig-templates) when you create a new project using the 

`create astro` CLI command. Both of Astro’s `strict` and `strictest` templates include the TypeScript settings your project needs for content collections.If you changed this setting to `base` because you are not writing TypeScript in your project, or are not using any of Astro’s built-in templates, you will need to also add the following `compilerOptions` in your `tsconfig.json` to use content collections:

## Defining build-time content collections

[Section titled “Defining build-time content collections”](#defining-build-time-content-collections)

All of your build-time content collections are defined in a special `src/content.config.ts` file (`.js` and `.mjs` extensions are also supported) using `defineCollection()`, and then a single collections object is exported for use in your project.

Each individual collection configures:

- [a build-time](#build-time-collection-loaders)for a data source (required)- `loader`
- [a build-time](#defining-the-collection-schema)for type safety (optional, but highly recommended!)- `schema`

You can then use the dedicated `getCollection()` and `getEntry()` functions to [query your content collections data](#querying-build-time-collections) and render your content.

You can choose to [generate page routes](#generating-routes-from-content) from your build-time collection entries at build time for an entirely static, prerendered site. Or, you can render your build-time collections on demand, choosing to delay building your page until it is first requested. This is useful when you have a large number of pages (e.g. thousands or tens of thousands) and want to delay building a static page until it is needed.

## Build-time collection loaders

[Section titled “Build-time collection loaders”](#build-time-collection-loaders)

Astro provides two built-in loaders (`glob()` and `file()`) for fetching your local content at build time. Pass the location of your data in your project or on your filesystem, and these loaders will automatically handle your data and update the persistent data store content layer.

To fetch remote data at build time, you can [build a custom loader](#custom-build-time-loaders) to retrieve your data and update the data store. Or, you can use any [third-party or community-published loader integration](https://astro.build/integrations/2/?search=&categories%5B%5D=loaders). Several already exist for popular content management systems as well as common data sources such as Obsidian vaults, GitHub repositories, or Bluesky posts.

### The `glob()` loader

[Section titled “The glob() loader”](#the-glob-loader)

The [ glob() loader](/en/reference/content-loader-reference/#glob-loader) fetches entries from directories of Markdown, MDX, Markdoc, JSON, YAML, or TOML files from anywhere on the filesystem. If you store your content entries locally as separate files, such as a directory of blog posts, then the 

`glob()` loader is all you need to access your content.This loader requires a `pattern` of entry files to match using glob patterns supported by [micromatch](https://github.com/micromatch/micromatch#matching-features), and a `base` file path of where your files are located. A unique `id` for each entry will be automatically generated from its file name, but you can [define custom IDs](#defining-custom-ids) if needed.

#### Defining custom IDs

[Section titled “Defining custom IDs”](#defining-custom-ids)

When using the [ glob() loader](#the-glob-loader) with Markdown, MDX, Markdoc, JSON, or TOML files, every content entry 

[is automatically generated in an URL-friendly format based on the content filename. This unique](/en/reference/modules/astro-content/#collectionentryid)

`id``id` is used to query the entry directly from your collection. It is also useful when [creating new pages and URLs from your content](#generating-routes-from-content).

You can override a single entry’s generated `id` by adding your own `slug` property to the file frontmatter or data object for JSON files. This is similar to the “permalink” feature of other web frameworks.

You can also pass options to the `glob()` loader’s [ generateID() helper function](/en/reference/content-loader-reference/#generateid) when you define your build-time collection to adjust how 

`id`s are generated. For example, you may wish to revert the default behavior of converting uppercase letters to lowercase for each collection entry:### The `file()` loader

[Section titled “The file() loader”](#the-file-loader)

The [ file() loader](/en/reference/content-loader-reference/#file-loader) fetches multiple entries from a single local file defined in your collection. The 

`file()` loader will automatically detect and parse (based on the file extension) a single array of objects from JSON and YAML files, and will treat each top-level table as an independent entry in TOML files.Each entry object in the file must have a unique `id` key property so that the entry can be identified and queried. Unlike the `glob()` loader, the `file()` loader will not automatically generate IDs for each entry.

You can provide your entries as an array of objects with an `id` property, or in object form where the unique `id` is the key:

#### Parsing other data formats

[Section titled “Parsing other data formats”](#parsing-other-data-formats)

Support for parsing single JSON, YAML, and TOML files into collection entries with the `file()` loader is built-in (unless you have a [nested JSON document](#nested-json-documents)). To load your collection from unsupported file types, such as `.csv`, you will need to create a [parser function](/en/reference/content-loader-reference/#parser). This function can be made async if required (e.g. to fetch files from the web, or if your parser is asynchronous).

The following example shows importing a third-party CSV parser then passing a custom `parser` function to the `file()` loader:

##### Nested `.json` documents

[Section titled “Nested .json documents”](#nested-json-documents)

The `parser()` argument can be used to load a single collection from a nested JSON document. For example, this JSON file contains multiple collections:

You can separate these collections by passing a custom `parser()` function to the `file()` loader for each collection, using Astro’s built-in JSON parsing:

### Custom build-time loaders

[Section titled “Custom build-time loaders”](#custom-build-time-loaders)

You can [build a custom loader](/en/reference/content-loader-reference/#building-a-loader) using the Content Loader API to fetch remote content from any data source, such as a CMS, a database, or an API endpoint.

Then you can import and define your custom loader in your collections config, passing any required values:

Find community-built and third-party loaders in the [Astro integrations directory](https://astro.build/integrations/?search=&categories%5B%5D=loaders).

Using a custom loader to fetch your data will automatically create a collection from your remote data. This gives you all the benefits of local collections, including collection-specific API helpers such as `getCollection()` and `render()` to [query and display your data](#querying-build-time-collections), as well as schema validation.

Similar to creating an Astro integration or Vite plugin, you can [distribute your loader as an npm package](/en/guides/integrations/) that others can use in their projects.

[Content Loader API](/en/reference/content-loader-reference/)for examples of how to build your own loader.

## Defining the collection schema

[Section titled “Defining the collection schema”](#defining-the-collection-schema)

Schemas enforce consistent frontmatter or entry data within a collection through Zod validation. A schema **guarantees** that this data exists in a predictable form when you need to reference or query it. If any file violates its collection schema, Astro will provide a helpful error to let you know.

Schemas also power Astro’s automatic TypeScript typings for your content. When you define a schema for your collection, Astro will automatically generate and apply a TypeScript interface to it. The result is full TypeScript support when you query your collection, including property autocompletion and type-checking.

In order for Astro to recognize a new or updated schema, you may need to restart the dev server or [sync the content layer](/en/reference/cli-reference/#astro-dev) (`s + enter`) to define the `astro:content` module.

Providing a `schema` is optional, but highly recommended! If you choose to use a schema, then every frontmatter or data property of your collection entries must be defined using a [Zod data type](/en/reference/modules/astro-zod/#common-data-type-validators):

### Defining datatypes with Zod

[Section titled “Defining datatypes with Zod”](#defining-datatypes-with-zod)

Astro uses [Zod](https://github.com/colinhacks/zod) to power its content schemas. With Zod, Astro is able to validate every file’s data within a collection *and* provide automatic TypeScript types when you query content from inside your project.

To use Zod in Astro, import the `z` utility from `"astro/zod"`. This is a re-export of the Zod library, and it supports all of the features of Zod 4.

[for a cheatsheet of common datatypes and to learn how Zod works and what features are available.](/en/reference/modules/astro-zod/)

`z` utility reference#### Zod schema methods

[Section titled “Zod schema methods”](#zod-schema-methods)

All [Zod schema methods](/en/reference/modules/astro-zod/#using-zod-methods) (e.g. `.parse()`, `.transform()`) are available, with some limitations. Notably, performing custom validation checks on images using `image().refine()` is unsupported.

### Defining collection references

[Section titled “Defining collection references”](#defining-collection-references)

Collection entries can also “reference” other related entries.

With the [ reference() function](/en/reference/modules/astro-content/#reference), you can define a property in a collection schema as an entry from another collection. For example, you can require that every 

`space-shuttle` entry includes a `pilot` property which uses the `pilot` collection’s own schema for type checking, autocomplete, and validation.A common example is a blog post that references reusable author profiles stored as JSON, or related post URLs stored in the same collection:

This example blog post specifies the `id`s of related posts and the `id` of the post author:

These references will be transformed into objects containing a `collection` key and an `id` key, allowing you to easily [query them in your templates](#accessing-referenced-data).

## Querying build-time collections

[Section titled “Querying build-time collections”](#querying-build-time-collections)

Astro provides helper functions to query a build-time collection and return one or more content entries.

- `getCollection()`
- `getEntry()`

These return entries with a unique `id`, a `data` object with all defined properties, and will also return a `body` containing the raw, uncompiled body of a Markdown, MDX, or Markdoc document.

The sort order of generated collections is non-deterministic and platform-dependent. This means that if you are calling `getCollection()` and need your entries returned in a specific order (e.g. blog posts sorted by date), you must sort the collection entries yourself:

[.](/en/reference/modules/astro-content/#collectionentry)

`CollectionEntry` type### Using content in Astro templates

[Section titled “Using content in Astro templates”](#using-content-in-astro-templates)

After querying your collections, you can access each entry’s content and metadata directly inside of your Astro component template.

For example, you can create a list of links to your blog posts, displaying information from your entry’s frontmatter using the `data` property:

### Rendering body content

[Section titled “Rendering body content”](#rendering-body-content)

Once queried, you can render Markdown and MDX entries to HTML using the [ render()](/en/reference/modules/astro-content/#render) function from 

`astro:content`. Calling this function gives you access to rendered HTML content, including both a `<Content />` component and a list of all rendered headings.[pass your own components to](/en/guides/integrations-guide/mdx/#passing-components-to-mdx-content)to replace HTML elements with custom alternatives.

`<Content />`#### Passing content as props

[Section titled “Passing content as props”](#passing-content-as-props)

A component can also pass an entire collection entry as a prop.

You can use the [ CollectionEntry](/en/reference/modules/astro-content/#collectionentry) utility to correctly type your component’s props using TypeScript. This utility takes a string argument that matches the name of your collection schema and will inherit all of the properties of that collection’s schema.

### Filtering collection queries

[Section titled “Filtering collection queries”](#filtering-collection-queries)

`getCollection()` takes an optional “filter” callback that allows you to filter your query based on an entry’s `id` or `data` properties.

You can use this to filter by any content criteria you like. For example, you can filter by properties like `draft` to prevent any draft blog posts from publishing to your blog:

You can also create draft pages that are available when running the dev server, but not built in production:

The filter argument also supports filtering by nested directories within a collection. Since the `id` includes the full nested path, you can filter by the start of each `id` to only return items from a specific nested directory:

### Accessing referenced data

[Section titled “Accessing referenced data”](#accessing-referenced-data)

To access [references defined in your schema](#defining-collection-references), first query your collection entry. Your references will be available on the returned `data` object. (e.g. `entry.data.author` and `entry.data.relatedPosts`)

Then, you can use the `getEntry()` function again (or `getEntries()` to retrieve multiple referenced entries) by passing those returned values. The `reference()` function in your schema transforms those values into one or more `collection` and `id` objects as a convenient way to query this related data.

## Generating Routes from Content

[Section titled “Generating Routes from Content”](#generating-routes-from-content)

Content collections are stored outside of the `src/pages/` directory. This means that no pages or routes are generated for your collection items by default by Astro’s [file-based routing](/en/guides/routing/).

You will need to manually create a new [dynamic route](/en/guides/routing/#dynamic-routes) if you want to generate HTML pages for each of your collection entries, such as individual blog posts. Your dynamic route will map the incoming request param (e.g. `Astro.params.id` in `src/pages/blog/[...id].astro`) to fetch the correct entry for each page.

The exact method for generating routes will depend on whether your pages are prerendered (default) or rendered on demand by a server.

### Building for static output (default)

[Section titled “Building for static output (default)”](#building-for-static-output-default)

If you are building a static website (Astro’s default behavior) with build-time collections, use the [ getStaticPaths()](/en/reference/routing-reference/#getstaticpaths) function to create multiple pages from a single page component (e.g. 

`src/pages/[id].astro`) during your build.Call `getCollection()` inside of `getStaticPaths()` to have your collection data available for building static routes. Then, create the individual URL paths using the `id` property of each content entry. Each page receives the entire collection entry as a prop for [use in your page template](#using-content-in-astro-templates).

This will generate a page route for every entry in the `blog` collection. For example, an entry at `src/blog/hello-world.md` will have an `id` of `hello-world`, and therefore its final URL will be `/posts/hello-world/`.

If your custom slugs contain the `/` character to produce URLs with multiple path segments, you must use a [rest parameter (e.g.  [...id])](/en/guides/routing/#rest-parameters) in the 

`.astro` filename for this dynamic routing page.### Building routes on demand at request time

[Section titled “Building routes on demand at request time”](#building-routes-on-demand-at-request-time)

With an adapter installed for [on-demand rendering](/en/guides/on-demand-rendering/), you can generate your dynamic page routes at request time. First, examine the request (using `Astro.request` or `Astro.params`) to find the slug on demand, and then fetch it using one of Astro’s content collection helper functions:

- `getEntry()`
- `getLiveEntry()`

Explore the `src/pages/` folder of the [blog tutorial demo code on GitHub](https://github.com/withastro/blog-tutorial-demo/tree/content-collections/src/pages) to see full examples of creating dynamic pages from your collections for blog features like a list of blog posts, tags pages, and more!

## Live content collections

[Section titled “Live content collections”](#live-content-collections)

Live collections use a different API than build-time content collections, although the configuration and helper functions are designed to feel familiar.

Key differences include:

- **Execution time**: Run at request time instead of build time
- **Configuration file**: Use- `src/live.config.ts`instead of- `src/content.config.ts`
- **Collection definition**: Use- `defineLiveCollection()`instead of- `defineCollection()`
- **Loader API**: Implement- `loadCollection`and- `loadEntry`methods instead of the- `load`method
- **Data return**: Return data directly instead of storing in the data store
- **User-facing functions**: Use- `getLiveCollection()`/- `getLiveEntry()`instead of- `getCollection()`/- `getEntry()`

Additionally, you must have an adapter configured for [on-demand rendering](/en/guides/on-demand-rendering/) of live collection data.

Define your live collections in the special file `src/live.config.ts` (separate from your `src/content.config.ts` for build-time collections, if you have one).

Each individual collection configures:

- a [live](#creating-a-live-loader)for your data source, and optionally for type safety (required)`loader`
- a [live collection](#using-zod-schemas-with-live-collections)for type safety (optional)`schema`

Unlike for build-time collections, there are no built-in live loaders available. You will need to [create a custom live loader](#creating-a-live-loader) for your specific data source or find a third-party loader to pass to your live collection’s `loader` property.

You can optionally [include type safety in your live loaders](/en/reference/content-loader-reference/#the-liveloader-object). Therefore, [defining a Zod  schema](#using-zod-schemas-with-live-collections) for live collections is optional. However, if you provide one, it will take precedence over the live loader’s types.

You can then use the dedicated `getLiveCollection()` and `getLiveEntry()` functions to [access your live data](#accessing-live-data) and render your content.

You can [generate page routes](#generating-routes-from-content) from your live collection entries on demand, fetching your data fresh at runtime upon each request without needing a rebuild of your site like [build-time collections](#defining-build-time-content-collections) do. This is useful when accessing live, up-to-the-moment data is more important than having your content available in a performant data storage layer that persists between site builds.

### Creating a live loader

[Section titled “Creating a live loader”](#creating-a-live-loader)

You can build a custom [live loader](/en/reference/content-loader-reference/#live-loaders) using the Live Loader API to fetch remote content fresh upon request from any data source, such as a CMS, a database or an API endpoint. You will have to tell your live loader how to fetch and return content entries from your desired data source, as well as provide error handling for unsuccessful data requests.

Using a live loader to fetch your data will automatically create a collection from your remote data. This gives you all the benefits of Astro’s content collections, including collection-specific API helpers such as `getLiveCollection()` and `render()` to [query and display your data](#querying-build-time-collections), as well as helpful error handling.

Find community-built and third-party live loaders in the [Astro integrations directory](https://astro.build/integrations/?search=&categories%5B%5D=loaders).

[building a live loader](/en/reference/content-loader-reference/#building-a-live-loader)using the Live Loader API

### Using Zod schemas with live collections

[Section titled “Using Zod schemas with live collections”](#using-zod-schemas-with-live-collections)

You can use Zod schemas with live collections to validate and transform data at runtime. This Zod validation works the same way as [schemas for build-time collections](#defining-the-collection-schema).

When you define a schema for a live collection, it takes precedence over [the live loader’s types](/en/reference/content-loader-reference/#the-liveloader-object) when you query the collection:

When using Zod schemas with live collections, validation errors are automatically caught and returned as `AstroError` objects:

[Zod’s README](https://github.com/colinhacks/zod)for complete documentation on how Zod works and what features are available.

### Accessing live data

[Section titled “Accessing live data”](#accessing-live-data)

Astro provides live collection helper functions to access live data on each request and return one (or more) content entries. These can be used similarly to their [build-time collection counterparts](#querying-build-time-collections).

- `getLiveCollection()`
- `getLiveEntry()`

These return entries with a unique `id`, and `data` object with all defined properties from the live loader. When using third-party or community loaders distributed as npm packages, check their own documentation for the expected shape of data returned.

You can use these functions to access your live data, passing the name of the collection and optionally filtering conditions.

#### Rendering content

[Section titled “Rendering content”](#rendering-content)

If your live loader [returns a  rendered property](/en/reference/content-loader-reference/#livedataentryrendered), you can use 

[the](#rendering-body-content)to render your content directly in your pages, using the same method as build-time collections.

`render()` function and `<Content />` componentYou also have access to any [error returned by the live loader](/en/reference/content-loader-reference/#error-handling-in-live-loaders), for example, to rewrite to a 404 page when content cannot be displayed:

#### Error handling

[Section titled “Error handling”](#error-handling)

Live loaders can fail due to network issues, API errors, or validation problems. The API is designed to make error handling explicit.

When you call `getLiveCollection()` or `getLiveEntry()`, the error will be one of:

- The error type defined by the loader (if it returned an error)
- A `LiveEntryNotFoundError`if the entry was not found
- A `LiveCollectionValidationError`if the collection data does not match the expected schema
- A `LiveCollectionCacheHintError`if the cache hint is invalid
- A `LiveCollectionError`for other errors, such as uncaught errors thrown in the loader

You can use `instanceof` to check the type of an error at runtime:

### Caching live data

[Section titled “Caching live data”](#caching-live-data)

	**Added in:**
	`astro@7.0.0`
	New
	

When live loaders provide [cache hints](/en/reference/content-loader-reference/#live-loaders), `getLiveEntry()` and `getLiveCollection()` return a `cacheHint` object. This allows you to control the [caching behavior](/en/guides/caching/) of your routes without manually setting headers.

Cache hints include [ tags](/en/reference/content-loader-reference/#cachehinttags) for targeted invalidation and 

[to keep cached data fresh. You can also combine the cache hints with your own](/en/reference/content-loader-reference/#cachehintlastmodified)

`lastModified`[cache options](/en/reference/cache-provider-reference/#cacheoptions)to further customize caching behavior.

See the [Content Loader Reference](/en/reference/content-loader-reference/) for more about implementing cache hints in your live loaders.

#### Entry-level cache hints

[Section titled “Entry-level cache hints”](#entry-level-cache-hints)

Pass the `cacheHint` returned by `getLiveEntry()` to [ Astro.cache.set()](/en/reference/api-reference/#cacheset) to apply the loader’s recommended caching strategy.

The following example passes the loader’s cache hint and adds a `maxAge` to control how long the response stays fresh:

You can also pass a [ LiveDataEntry](/en/reference/content-loader-reference/#livedataentry) directly to let Astro extract its 

`cacheHint` automatically:#### Collection-level cache hints

[Section titled “Collection-level cache hints”](#collection-level-cache-hints)

When fetching a full collection with `getLiveCollection()`, Astro merges cache hints from the collection response and all individual entries: tags are accumulated, and the most recent `lastModified` wins.

The following example passes the merged cache hint from a collection and sets a 10-minute freshness window:

#### Invalidating by entry

[Section titled “Invalidating by entry”](#invalidating-by-entry)

You can invalidate cached entries by passing a `LiveDataEntry` to [ cache.invalidate()](/en/reference/api-reference/#cacheinvalidate). This allows you to target specific cached responses for invalidation based on the entry’s cache tags, without needing to clear the entire cache.

The following example invalidates the cached response for a specific product entry:

## Using JSON Schema files in your editor

[Section titled “Using JSON Schema files in your editor”](#using-json-schema-files-in-your-editor)

	**Added in:**
	`astro@4.13.0`
	
	

Astro auto-generates [JSON Schema](https://json-schema.org/) files for collections, which you can use in your editor to get IntelliSense and type-checking for data files.

A JSON Schema file is generated for each collection in your project and output to the `.astro/collections/` directory.
For example, if you have two collections, one named `authors` and another named `posts`, Astro will generate `.astro/collections/authors.schema.json` and `.astro/collections/posts.schema.json`.

### Use JSON Schemas in JSON files

You can manually point to an Astro-generated schema by setting the `$schema` field in your JSON file.
The value should be a relative file path from the data file to the schema.
In the following example, a data file in `src/data/authors/` uses the schema generated for the `authors` collection:

#### Use a schema for a group of JSON files in VS Code

In VS Code, you can configure a schema to apply to all files in a collection using the [ json.schemas setting](https://code.visualstudio.com/docs/languages/json#_json-schemas-and-settings).
In the following example, all files in the 

`src/data/authors/` directory will use the schema generated for the `authors` collection:### Use schemas in YAML files in VS Code

In VS Code, you can add support for using JSON schemas in YAML files using the [Red Hat YAML](https://marketplace.visualstudio.com/items?itemName=redhat.vscode-yaml) extension.
With this extension installed, you can reference a schema in a YAML file using a special comment syntax:

#### Use schemas for a group of YAML files in VS Code

With the Red Hat YAML extension, you can configure a schema to apply to all YAML files in a collection using the `yaml.schemas` setting.
In the following example, all YAML files in the `src/data/authors/` directory will use the schema generated for the `authors` collection:

See [“Associating schemas”](https://marketplace.visualstudio.com/items?itemName=redhat.vscode-yaml#associating-schemas) in the Red Hat YAML extension documentation for more details.

[Contribute](/en/contribute/)

[Community](https://astro.build/chat)

[Sponsor](https://opencollective.com/astrodotbuild)

# Citations

1. Source page: https://docs.astro.build/en/guides/content-collections
