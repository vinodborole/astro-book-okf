---
type: Web Page
title: Using environment variables | Docs
description: Learn how to use environment variables in an Astro project.
resource: https://docs.astro.build/en/guides/environment-variables
timestamp: '2026-07-13T09:18:12.222139+00:00'
---

# Using environment variables

Astro gives you access to [Vite’s built-in environment variables support](#vites-built-in-support) and includes some [default environment variables for your project](#default-environment-variables) that allow you to access configuration values for your current project (e.g. `site`, `base`), whether your project is running in development or production, and more.

Astro also provides a way to [use and organize your environment variables with type safety](#type-safe-environment-variables). It is available for use inside the Astro context (e.g. Astro components, routes and endpoints, UI framework components, middleware), and managed with [a schema in your Astro configuration](/en/reference/configuration-reference/#env).

## Vite’s built-in support

[Section titled “Vite’s built-in support”](#vites-built-in-support)

Astro uses Vite’s built-in support for environment variables, which are statically replaced at build time, and lets you [use any of its methods](https://vite.dev/guide/env-and-mode.html) to work with them.

Note that while *all* environment variables are available in server-side code, only environment variables prefixed with `PUBLIC_` are available in client-side code for security purposes.

In this example, `PUBLIC_ANYBODY` (accessible via `import.meta.env.PUBLIC_ANYBODY`) will be available in server or client code, while `SECRET_PASSWORD` (accessible via `import.meta.env.SECRET_PASSWORD`) will be server-side only.

`.env` files are not loaded inside [configuration files](#in-the-astro-config-file).

### IntelliSense for TypeScript

[Section titled “IntelliSense for TypeScript”](#intellisense-for-typescript)

By default, Astro provides a type definition for `import.meta.env` in `astro/client.d.ts`.

While you can define more custom env variables in `.env.[mode]` files, you may want to get TypeScript IntelliSense for user-defined env variables which are prefixed with `PUBLIC_`.

To achieve this, you can create an `env.d.ts` in `src/` to [extend the global types](/en/guides/typescript/#extending-global-types) and configure `ImportMetaEnv` like this:

## Default environment variables

[Section titled “Default environment variables”](#default-environment-variables)

Astro includes a few environment variables out of the box:

- `import.meta.env.MODE`: The mode your site is running in. This is- `development`when running- `astro dev`and- `production`when running- `astro build`.
- `import.meta.env.PROD`:- `true`if your site is running in production;- `false`otherwise.
- `import.meta.env.DEV`:- `true`if your site is running in development;- `false`otherwise. Always the opposite of- `import.meta.env.PROD`.
- `import.meta.env.BASE_URL`: The base URL your site is being served from. This is determined by the- `base`config option
- `import.meta.env.SITE`: This is set to- [the](/en/reference/configuration-reference/#site)specified in your project’s- `site`option- `astro.config`.

Use them like any other environment variable.

## Setting environment variables

[Section titled “Setting environment variables”](#setting-environment-variables)

`.env` files

[Section titled “.env files”](#env-files)

Environment variables can be loaded from `.env` files in your project directory.

Just create a `.env` file in the project directory and add some variables to it.

You can also add `.production`, `.development` or a custom mode name to the filename itself (e.g `.env.testing`, `.env.staging`). This allows you to use different sets of environment variables at different times.

The `astro dev` and `astro build` commands default to `"development"` and `"production"` modes, respectively. You can run these commands with the [ --mode flag](/en/reference/cli-reference/#--mode-string) to pass a different value for 

`mode` and load the matching `.env` file.This allows you to run the dev server or build your site connecting to different APIs:

For more on `.env` files, [see the Vite documentation](https://vite.dev/guide/env-and-mode.html#env-files).

### In the Astro config file

[Section titled “In the Astro config file”](#in-the-astro-config-file)

Astro evaluates configuration files before it loads your other files. This means that you cannot use `import.meta.env` in `astro.config.mjs` to access environment variables that were set in `.env` files.

You can use `process.env` in a configuration file to access other environment variables, like those [set by the CLI](#using-the-cli).

You can also use [Vite’s  loadEnv helper](https://main.vite.dev/config/#using-environment-variables-in-config) to manually load 

`.env` files.`pnpm` does not allow you to import modules that are not directly installed in your project. If you are using `pnpm`, you will need to install `vite` to use the `loadEnv` helper.

### Using the CLI

[Section titled “Using the CLI”](#using-the-cli)

You can also add environment variables as you run your project:

## Getting environment variables

[Section titled “Getting environment variables”](#getting-environment-variables)

Environment variables in Astro are accessed with `import.meta.env`, using the [ import.meta feature added in ES2020](https://tc39.es/ecma262/2020/#prod-ImportMeta), instead of 

`process.env`.For example, use `import.meta.env.PUBLIC_POKEAPI` to get the `PUBLIC_POKEAPI` environment variable.

When using SSR, environment variables can be accessed at runtime based on the SSR adapter being used. With most adapters you can access environment variables with `process.env`, but some adapters work differently. For the Deno adapter, you will use `Deno.env.get()`. See how to [access the Cloudflare runtime](/en/guides/integrations-guide/cloudflare/#cloudflare-runtime) to handle environment variables when using the Cloudflare adapter. Astro will first check the server environment for variables, and if they don’t exist, Astro will look for them in `.env` files.

## Type safe environment variables

[Section titled “Type safe environment variables”](#type-safe-environment-variables)

The `astro:env` API lets you configure a type-safe schema for [environment variables you have set](#setting-environment-variables). This allows you to indicate whether they should be available on the server or the client, and define their data type and additional properties.

[make an adapter compatible with](/en/reference/adapter-reference/#envgetsecret).

`astro:env`### Basic Usage

[Section titled “Basic Usage”](#basic-usage)

#### Define your schema

[Section titled “Define your schema”](#define-your-schema)

To configure a schema, add the `env.schema` option to your Astro config:

You can then [register variables as a string, number, enum, or boolean](#data-types) using the `envField` helper. Define the [kind of environment variable](#variable-types) by providing a `context` (`"client"` or `"server"`) and `access` (`"secret"` or `"public"`) for each variable, and pass any additional properties such as `optional` or `default` in an object:

Types will be generated for you when running `astro dev` or `astro build`, but you can run `astro sync` to generate types only.

#### Use variables from your schema

[Section titled “Use variables from your schema”](#use-variables-from-your-schema)

Import and use your defined variables from the appropriate `/client` or `/server` module:

### Variable types

[Section titled “Variable types”](#variable-types)

There are three kinds of environment variables, determined by the combination of `context` (`"client"` or `"server"`) and `access` (`"secret"` or `"public"`) settings defined in your schema:

- 
**Public client variables**: These variables end up in both your final client and server bundles, and can be accessed from both client and server through the`astro:env/client`module:
- 
**Public server variables**: These variables end up in your final server bundle and can be accessed on the server through the`astro:env/server`module:
- 
**Secret server variables**: These variables are not part of your final bundle and can be accessed on the server through the`astro:env/server`module:By default, all secrets are validated whenever anything is imported from the `astro:env/server`module. This means, secrets may be validated even when they are not imported. You may need to[pass dummy environment variables](#setting-environment-variables)to satisfy this validation during the build.You can also enable validating secrets on start by [configuring](/en/reference/configuration-reference/#envvalidatesecrets).`validateSecrets: true`

**Secret client variables** are not supported because there is no safe way to send this data to the client. Therefore, it is not possible to configure both `context: "client"` and `access: "secret"` in your schema.

### Data types

[Section titled “Data types”](#data-types)

There are currently four data types supported: strings, numbers, enums, and booleans:

[.](/en/reference/modules/astro-config/#envfield)

`envField` API reference### Retrieving secrets dynamically

[Section titled “Retrieving secrets dynamically”](#retrieving-secrets-dynamically)

Despite defining your schema, you may want to retrieve the raw value of a given secret or to retrieve secrets not defined in your schema. In this case, you can use `getSecret()` exported from `astro:env/server`:

[the API reference](/en/reference/modules/astro-env/#getsecret).

### Limitations

[Section titled “Limitations”](#limitations)

`astro:env` is a virtual module which means it can only be used inside the Astro context. For example, you can use it in:

- Middlewares
- Astro routes and endpoints
- Astro components
- Framework components
- Modules

You cannot use it in the following and will have to resort to `process.env`:

- `astro.config.mjs`
- Scripts

[Contribute](/en/contribute/)

[Community](https://astro.build/chat)

[Sponsor](https://opencollective.com/astrodotbuild)

# Citations

1. Source page: https://docs.astro.build/en/guides/environment-variables
