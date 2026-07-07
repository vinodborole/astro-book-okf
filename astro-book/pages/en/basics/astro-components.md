---
type: Web Page
title: Components | Docs
description: An introduction to Astro components.
resource: https://docs.astro.build/en/basics/astro-components
timestamp: '2026-07-07T10:59:34.007706+00:00'
---

# Components

**Astro components** are the basic building blocks of any Astro project. They are HTML-only templating components with no client-side runtime and use the `.astro` file extension.

If you know HTML, you already know enough to write your first Astro component.

Astro components are extremely flexible. An Astro component can be as small as a snippet of HTML, like a collection of common `<meta>` tags that make SEO easy to work with. Components can be reusable UI elements, like a header or a profile card. Astro components can even contain an entire page layout or, when located in the special `src/pages/` folder, be an entire page itself.

The most important thing to know about Astro components is that they **don’t render on the client**. They render to HTML either at build-time or on-demand. You can include JavaScript code inside of your component frontmatter, and all of it will be stripped from the final page sent to your users’ browsers. The result is a faster site, with zero JavaScript footprint added by default.

When your Astro component does need client-side interactivity, you can add standard HTML `<script>` tags or UI Framework components as “client islands”.

For components that need to render personalized or dynamic content, you can defer their server rendering by adding a server directive. These “server islands” will render their content when it is available, without delaying the entire page load.

## Component Structure

Section titled “Component Structure”An Astro component is made up of two main parts: the **Component Script** and the **Component Template**. Each part performs a different job, but together they provide a framework that is both easy to use and expressive enough to handle whatever you might want to build.

### The Component Script

Section titled “The Component Script”Astro uses a code fence (`---`) to identify the component script in your Astro component. If you’ve ever written Markdown before, you may already be familiar with a similar concept called *frontmatter.* Astro’s idea of a component script was directly inspired by this concept.

You can use the component script to write any JavaScript code that you need to render your template. This can include:

- importing other Astro components
- importing other framework components, like React
- importing data, like a JSON file
- fetching content from an API or database
- creating variables that you will reference in your template

The code fence is designed to guarantee that the JavaScript that you write in it is “fenced in.” It won’t escape into your frontend application, or fall into your user’s hands. You can safely write code here that is expensive or sensitive (like a call to your private database) without worrying about it ever ending up in your user’s browser.

The Astro component script is TypeScript, which allows you to add additional syntax to JavaScript for editor tooling, and error checking.

### The Component Template

Section titled “The Component Template”The component template is below the code fence and determines the HTML output of your component.

If you write plain HTML here, your component will render that HTML in any Astro page it is imported and used.

However, Astro’s component template syntax also supports **JavaScript expressions**, Astro `<style>` and `<script>` tags, **imported components**, and **special Astro directives**. Data and values defined in the component script can be used in the component template to produce dynamically-created HTML.

## Component-based design

Section titled “Component-based design”Components are designed to be **reusable** and **composable**. You can use components inside of other components to build more and more advanced UI. For example, a `Button` component could be used to create a `ButtonGroup` component:

## Component Props

Section titled “Component Props”An Astro component can define and accept props. These props then become available to the component template for rendering HTML. Props are available on the `Astro.props` global in your frontmatter script.

Here is an example of a component that receives a `greeting` prop and a `name` prop. Notice that the props to be received are destructured from the global `Astro.props` object.

This component, when imported and rendered in other Astro components, layouts or pages, can pass these props as attributes:

You can also define your props with TypeScript with a `Props` type interface. Astro will automatically pick up the `Props` interface in your frontmatter and give type warnings/errors. These props can also be given default values when destructured from `Astro.props`.

Component props can be given default values to use when none are provided.

The `<slot />` element is a placeholder for external HTML content, allowing you to inject (or “slot”) child elements from other files into your component template.

By default, all child elements passed to a component will be rendered in its `<slot />`.

Unlike *props*, which are attributes passed to an Astro component available for use throughout your component with `Astro.props`, *slots* render child HTML elements where they are written.

This pattern is the basis of an Astro layout component: an entire page of HTML content can be “wrapped” with `<SomeLayoutComponent></SomeLayoutComponent>` tags and sent to the component to render inside of common page elements defined there.

`Astro.slots` utility functions for more ways to access and render slot content.
### Named Slots

Section titled “Named Slots”An Astro component can also have named slots. This allows you to pass only HTML elements with the corresponding slot name into a slot’s location.

Slots are named using the `name` attribute:

To inject HTML content into a particular slot, use the `slot` attribute on any child element to specify the name of the slot. All other child elements of the component will be injected into the default (unnamed) `<slot />`.

Use a `slot="my-slot"` attribute on the child element that you want to pass through to a matching `<slot name="my-slot" />` placeholder in your component.

To pass multiple HTML elements into a component’s `<slot/>` placeholder without a wrapping `<div>`, use the `slot=""` attribute on Astro’s `<Fragment/>` component:

Inject multiple rows and columns of HTML content using a `slot=""` attribute to specify the `"header"` and `"body"` content. Individual HTML elements can also be styled:

Note that named slots must be an immediate child of the component. You cannot pass named slots through nested elements.

Named slots can also be passed to UI framework components!

It is not possible to dynamically generate an Astro slot name, such as within a map function. If this feature is needed within UI framework components, it might be best to generate these dynamic slots within the framework itself.

### Fallback Content for Slots

Section titled “Fallback Content for Slots”Slots can also render **fallback content**. When there are no matching children passed to a slot, a `<slot />` element will render its own placeholder children.

Fallback content will only be displayed when there are no matching elements with the `slot="name"` attribute being passed in to a named slot.

Astro will pass an empty slot when a slot element exists but has no content to pass. Fallback content cannot be used as a default when an empty slot is passed. Fallback content is only displayed when no slot element can be found.

### Transferring slots

Section titled “Transferring slots”Slots can be transferred to other components. For example, when creating nested layouts:

Named slots can be transferred to another component using both the `name` and `slot` attributes on a `<slot />` tag.

Now, the default and `head` slots passed to `HomeLayout` will be transferred to the `BaseLayout` parent.

## HTML Components

Section titled “HTML Components”Astro supports importing and using `.html` files as components or placing these files within the `src/pages/` subdirectory as pages. You may want to use HTML components if you’re reusing code from an existing site built without a framework, or if you want to ensure that your component has no dynamic features.

HTML components must contain only valid HTML, and therefore lack key Astro component features:

- They don’t support frontmatter, server-side imports, or dynamic expressions.
- Any `<script>`tags are left unbundled, treated as if they had an`is:inline`directive.
- They can only reference assets that are in the `public/`folder.

A `<slot />` element inside an HTML component will work as it would in an Astro component. In order to use the HTML Web Component Slot element instead, add `is:inline` to your `<slot>` element.

# Citations

1. Source page: https://docs.astro.build/en/basics/astro-components
