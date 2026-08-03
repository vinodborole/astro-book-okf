---
type: Web Page
title: Front-end frameworks | Docs
description: Build your Astro website with React, Svelte, and more.
resource: https://docs.astro.build/en/guides/framework-components
timestamp: '2026-08-03T09:35:37.104348+00:00'
---

# Front-end frameworks

Build your Astro website without sacrificing your favorite component framework. Create Astro [islands](/en/concepts/islands/) with the UI frameworks of your choice.

## Official front-end framework integrations

[Section titled “Official front-end framework integrations”](#official-front-end-framework-integrations)

Astro supports a variety of popular frameworks including [React](https://react.dev/), [Preact](https://preactjs.com/), [Svelte](https://svelte.dev/), [Vue](https://vuejs.org/), [SolidJS](https://www.solidjs.com/), and [AlpineJS](https://alpinejs.dev/) with official integrations.

Find even more [community-maintained framework integrations](https://astro.build/integrations/?search=&categories%5B%5D=frameworks) (e.g. Angular, Qwik, Elm) in our integrations directory.

### Front-end frameworks

## Installing integrations

[Section titled “Installing integrations”](#installing-integrations)

One or several of these Astro integrations can be installed and configured in your project.

See the [Integrations Guide](/en/guides/integrations/) for more details on installing and configuring Astro integrations.

Want to see an example for the framework of your choice? Visit [astro.new](https://astro.new/latest/frameworks) and select one of the framework templates.

## Using framework components

[Section titled “Using framework components”](#using-framework-components)

Use your JavaScript framework components in your Astro pages, layouts and components just like Astro components! All your components can live together in `/src/components`, or can be organized in any way you like.

To use a framework component, import it from its relative path in your Astro component script. Then, use the component alongside other components, HTML elements and JSX-like expressions in the component template.

By default, your framework components will only render on the server, as static HTML. This is useful for templating components that are not interactive and avoids sending any unnecessary JavaScript to the client.

## Hydrating interactive components

[Section titled “Hydrating interactive components”](#hydrating-interactive-components)

A framework component can be made interactive (hydrated) using a [`client:*` directive](/en/reference/directives-reference/#client-directives). These are component attributes that determine when your component’s JavaScript should be sent to the browser.

With all client directives except `client:only`, your component will first render on the server to generate static HTML. Component JavaScript will be sent to the browser according to the directive you chose. The component will then hydrate and become interactive.

The JavaScript framework (React, Svelte, etc.) needed to render the component will be sent to the browser along with the component’s own JavaScript. If two or more components on a page use the same framework, the framework will only be sent once.

Most framework-specific accessibility patterns should work the same when these components are used in Astro. Be sure to choose a client directive that will ensure any accessibility-related JavaScript is properly loaded and executed at the appropriate time!

### Available hydration directives

[Section titled “Available hydration directives”](#available-hydration-directives)

There are several hydration directives available for UI framework components: `client:load`, `client:idle`, `client:visible`, `client:media={QUERY}` and `client:only={FRAMEWORK}`.

[directives reference](/en/reference/directives-reference/#client-directives)page for a full description of these hydration directives, and their usage.

## Mixing frameworks

[Section titled “Mixing frameworks”](#mixing-frameworks)

You can import and render components from multiple frameworks in the same Astro component.

Astro will recognize and render your component based on its file extension. To distinguish between frameworks that use the same file extension, [additional configuration when rendering multiple JSX frameworks](/en/guides/integrations-guide/react/#combining-multiple-jsx-frameworks) (e.g. React and Preact) is required.

Only **Astro** components (`.astro`) can contain components from multiple frameworks.

## Passing props to framework components

[Section titled “Passing props to framework components”](#passing-props-to-framework-components)

You can pass props from Astro components to framework components:

Props that are passed to interactive framework components [using a `client:*` directive](/en/reference/directives-reference/#client-directives) must be [serialized](https://developer.mozilla.org/en-US/docs/Glossary/Serialization): translated into a format suitable for transfer over a network, or storage. However, Astro does not serialize every type of data structure. Therefore, there are some limitations on what can be passed as props to hydrated components.

The following prop types are supported:
plain object, `number`, `string`, `Array`, `Map`, `Set`, `RegExp`, `Date`, `BigInt`, `URL`, `Uint8Array`, `Uint16Array`, `Uint32Array`, and `Infinity`

Non-supported data structures passed to components, such as functions, can only be used during the component’s server rendering and cannot be used to provide interactivity. For example, passing functions to hydrated components is not supported because Astro cannot pass functions from the server in a way that makes them executable on the client.

## Passing children to framework components

[Section titled “Passing children to framework components”](#passing-children-to-framework-components)

Inside of an Astro component, you **can** pass children to framework components. Each framework has its own patterns for how to reference these children: React, Preact, and Solid all use a special prop named `children`, while Svelte and Vue use the `<slot />` element.

Additionally, you can use [Named Slots](/en/basics/astro-components/#named-slots) to group specific children together.

For React, Preact, and Solid, these slots will be converted to a top-level prop. Slot names using `kebab-case` will be converted to `camelCase`.

For Svelte and Vue these slots can be referenced using a `<slot>` element with the `name` attribute. Slot names using `kebab-case` will be preserved.

## Nesting framework components

[Section titled “Nesting framework components”](#nesting-framework-components)

Inside of an Astro file, framework component children can also be hydrated components. This means that you can recursively nest components from any of these frameworks.

Remember: framework component files themselves (e.g. `.jsx`, `.svelte`) cannot mix multiple frameworks.

This allows you to build entire “apps” in your preferred JavaScript framework and render them, via a parent component, to an Astro page.

Astro components are always rendered to static HTML, even when they include framework components that are hydrated. This means that you can only pass props that don’t do any HTML rendering. Passing React’s “render props” to framework components from an Astro component will not work, because Astro components can’t provide the client runtime behavior that this pattern requires. Instead, use named slots.

## Can I use Astro components inside my framework components?

[Section titled “Can I use Astro components inside my framework components?”](#can-i-use-astro-components-inside-my-framework-components)

Any UI framework component becomes an “island” of that framework. These components must be written entirely as valid code for that framework, using only its own imports and packages. You cannot import `.astro` components in a UI framework component (e.g. `.jsx` or `.svelte`).

You can, however, use [the Astro `<slot />` pattern](/en/basics/astro-components/#slots) to pass static content generated by Astro components as children to your framework components **inside an `.astro` component**.

## Can I hydrate Astro components?

[Section titled “Can I hydrate Astro components?”](#can-i-hydrate-astro-components)

If you try to hydrate an Astro component with a `client:` modifier, you will get an error.

[Astro components](/en/basics/astro-components/) are HTML-only templating components with no client-side runtime. But, you can use a `<script>` tag in your Astro component template to send JavaScript to the browser that executes in the global scope.

[client-side](/en/guides/client-side-scripts/)

`<script>` tags in Astro components
[Contribute](/en/contribute/)

[Community](https://astro.build/chat)

[Sponsor](https://opencollective.com/astrodotbuild)

# Citations

1. Source page: https://docs.astro.build/en/guides/framework-components
