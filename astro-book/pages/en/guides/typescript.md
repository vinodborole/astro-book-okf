---
type: Web Page
title: TypeScript | Docs
description: Learn how to use Astro's built-in TypeScript support.
resource: https://docs.astro.build/en/guides/typescript
timestamp: '2026-07-07T10:59:34.007706+00:00'
---

# TypeScript

Astro ships with built-in support for TypeScript. You can import `.ts` and `.tsx` files in your Astro project, write TypeScript code directly inside your Astro component, and even use an `astro.config.ts` file for your Astro configuration if you like.

Using TypeScript, you can prevent errors at runtime by defining the shapes of objects and components in your code. For example, if you use TypeScript to type your component’s props, you’ll get an error in your editor if you set a prop that your component doesn’t accept.

You don’t need to write TypeScript code in your Astro projects to benefit from it. Astro always treats your component code as TypeScript, and the Astro VS Code Extension will infer as much as it can to provide autocompletion, hints, and errors in your editor.

The Astro dev server won’t perform any type checking, but you can use a separate script to check for type errors from the command line.

Astro starter projects include a `tsconfig.json` file in your project. Even if you don’t write TypeScript code, this file is important so that tools like Astro and VS Code know how to understand your project. Some features (like npm package imports) aren’t fully supported in the editor without a `tsconfig.json` file. If you install Astro manually, be sure to create this file yourself.

### TSConfig templates

Section titled “TSConfig templates”Three extensible `tsconfig.json` templates are included in Astro: `base`, `strict`, and `strictest`. The `base` template enables support for modern JavaScript features and is also used as a basis for the other templates. We recommend using `strict` or `strictest` if you plan to write TypeScript in your project. You can view and compare the three template configurations at astro/tsconfigs/.

To inherit from one of the templates, use the `extends` setting:

Additionally, we recommend setting `include` and `exclude` as follows to benefit from Astro types and avoid checking built files:

### TypeScript editor plugin

Section titled “TypeScript editor plugin”The Astro TypeScript plugin can be installed separately when you are not using the official Astro VS Code extension. This plugin is automatically installed and configured by the VS Code extension, and you do not need to install both.

This plugin runs only in the editor. When running `tsc` in the terminal, `.astro` files are ignored entirely. Instead, you can use the `astro check` CLI command to check both `.astro` and `.ts` files.

This plugin also supports importing `.astro` files from `.ts` files (which can be useful for re-exporting).

Then, add the following to your `tsconfig.json`:

To check that the plugin is working, create a `.ts` file and import an Astro component into it. You should have no warning messages from your editor.

### UI Frameworks

Section titled “UI Frameworks”If your project uses a UI framework, additional settings depending on the framework might be needed. Please see your framework’s TypeScript documentation for more information. (Vue, React, Preact, Solid, Svelte)

## Type Imports

Section titled “Type Imports”Use explicit type imports and exports whenever possible.

This way, you avoid edge cases where Astro’s bundler may try to incorrectly bundle your imported types as if they were JavaScript.

You can configure TypeScript to enforce type imports in your `tsconfig.json` file. Set `verbatimModuleSyntax` to `true`. TypeScript will check your imports and tell you when `import type` should be used. This setting is enabled by default in all our presets.

## Import Aliases

Section titled “Import Aliases”Astro supports import aliases that you define in your `tsconfig.json` `paths` configuration. Read our imports guide to learn more.

## Extending global types

Section titled “Extending global types”You can create `src/env.d.ts` as a convention for adding custom types declarations, or to benefit from Astro types if you don’t have a `tsconfig.json`:

`window` and `globalThis`

Section titled “window and globalThis”You may want to add a property to the global object. You can do this by adding top-level declarations using the `declare` keyword to your `env.d.ts` file:

This will provide typing to `globalThis.myString` and `globalThis.myFunction`, as well as `window.myString` and `window.myFunction`.

Note that `window` is only available in client-side code. `globalThis` is available both server-side and client-side, but its server-side value won’t be shared with the client.

If you only want to type a property on the `window` object, provide a `Window` interface instead:

### Add non-standard attributes

Section titled “Add non-standard attributes”You may want to define a type for custom attributes or CSS properties. You can extend the default JSX definitions to add non-standard attributes by redeclaring the `astroHTML.JSX` namespace in a `.d.ts` file.

`astroHTML` is injected globally inside `.astro` components. To use it in TypeScript files, use a triple-slash directive:

### Using imports

Section titled “Using imports”You may want to extend global types by reusing types declared elsewhere in your project or from an external library. To do this, use dynamic imports:

A `.d.ts` file is an ambient module declaration. While its syntax is similar to ES modules, these files do not allow top-level imports/exports. If TypeScript encounters one, the file will be considered a module augmentation and this will break your global types.

## Component Props

Section titled “Component Props”Astro supports typing your component props via TypeScript. To enable, add a TypeScript `Props` interface to your component frontmatter. An `export` statement may be used, but is not necessary. The Astro VS Code Extension will automatically look for the `Props` interface and give you proper TS support when you use that component inside another template.

### Common prop type patterns

Section titled “Common prop type patterns”- If your component takes no props or slotted content, you can use `type Props = Record<string, never>`.
- If your component must be passed children to its default slot, you can enforce this by using `type Props = { children: any; };`.

## Type Utilities

Section titled “Type Utilities”
	**Added in:**
	`astro@1.6.0`
	
	

Astro comes with some built-in utility types for common prop type patterns. These are available under the `astro/types` entrypoint.

### Built-in HTML attributes

Section titled “Built-in HTML attributes”Astro provides the `HTMLAttributes` type to check that your markup is using valid HTML attributes. You can use these types to help build component props.

For example, if you were building a `<Link>` component, you could do the following to mirror the default HTML attributes for `<a>` tags in your component’s prop types.

`ComponentProps` type

Section titled “ComponentProps type”
	**Added in:**
	`astro@4.3.0`
	
	

This type export allows you to reference the `Props` accepted by another component, even if that component doesn’t export that `Props` type directly.

The following example shows using the `ComponentProps` utility from `astro/types` to reference a `<Button />` component’s `Props` types:

### Polymorphic type

Section titled “Polymorphic type”
	**Added in:**
	`astro@2.5.0`
	
	

Astro includes a helper to make it easier to build components that can render as different HTML elements with full type safety. This is useful for components like `<Link>` that can render as either `<a>` or `<button>` depending on the props passed to it.

The example below implements a fully-typed, polymorphic component that can render as any HTML element. The `HTMLTag` type is used to ensure that the `as` prop is a valid HTML element.

### Infer `getStaticPaths()` types

Section titled “Infer getStaticPaths() types”
	**Added in:**
	`astro@2.1.0`
	
	

Astro includes helpers for working with the types returned by your `getStaticPaths()` function for dynamic routes.

You can get the type of `Astro.params` with `InferGetStaticParamsType` and the type of `Astro.props` with `InferGetStaticPropsType` or you can use `GetStaticPaths` to infer both at once:

## Type checking

Section titled “Type checking”To see type errors in your editor, please make sure that you have the Astro VS Code extension installed. Please note that the `astro start` and `astro build` commands will transpile the code with esbuild, but will not run any type checking. To prevent your code from building if it contains TypeScript errors, change your “build” script in `package.json` to the following:

`astro check` checks all the files included in your TypeScript project. To check types within Svelte and Vue files, you can use the `svelte-check` and the `vue-tsc` packages respectively.

`.ts` file imports in Astro.
## Troubleshooting

Section titled “Troubleshooting”### Errors typing multiple JSX frameworks at the same time

Section titled “Errors typing multiple JSX frameworks at the same time”An issue may arise when using multiple JSX frameworks in the same project, as each framework requires different, sometimes conflicting, settings inside `tsconfig.json`.

**Solution**: Set the `jsxImportSource` setting to `react` (default), `preact` or `solid-js` depending on your most-used framework. Then, use a pragma comment inside any conflicting file from a different framework.

For the default setting of `jsxImportSource: react`, you would use:

# Citations

1. Source page: https://docs.astro.build/en/guides/typescript
