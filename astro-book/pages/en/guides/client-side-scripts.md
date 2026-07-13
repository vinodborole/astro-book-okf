---
type: Web Page
title: Scripts and event handling | Docs
description: How to add client-side interactivity to Astro components using native
  browser JavaScript APIs.
resource: https://docs.astro.build/en/guides/client-side-scripts
timestamp: '2026-07-13T09:18:12.222139+00:00'
---

# Scripts and event handling

You can send JavaScript to the browser and add functionality to your Astro components using `<script>` tags in the component template.

Scripts add interactivity to your site, such as handling events or updating content dynamically, without the need for a [UI framework](/en/guides/framework-components/) like React, Svelte, or Vue. This avoids the overhead of shipping framework JavaScript and doesn’t require you to know any additional framework to create a full-featured website or application.

## Client-Side Scripts

[Section titled “Client-Side Scripts”](#client-side-scripts)

Scripts can be used to add event listeners, send analytics data, play animations, and everything else JavaScript can do on the web.

Astro automatically enhances the HTML standard `<script>` tag with bundling, TypeScript, and more. See [how astro processes scripts](#script-processing) for more details.

[when your scripts will not be processed](#unprocessed-scripts)to troubleshoot script behavior, or to learn how to opt-out of this processing intentionally.

## Script processing

[Section titled “Script processing”](#script-processing)

By default, Astro processes `<script>` tags that contain no attributes (other than `src`) in the following ways:

- **TypeScript support:**All scripts are TypeScript by default.
- **Import bundling:**Import local files or npm modules, which will be bundled together.
- **Type Module:**Processed scripts become- `type="module"`
- **Deduplication:**If a component that contains a- `<script>`is used multiple times on a page, the script will only be included once.
- **Automatic inlining:**If the script is small enough, Astro will inline it directly into the HTML to reduce the number of requests.

### Unprocessed scripts

[Section titled “Unprocessed scripts”](#unprocessed-scripts)

Astro will not process a `<script>` tag if it has any attribute other than `src`.

You can add the [ is:inline](/en/reference/directives-reference/#isinline) directive to intentionally opt out of processing for a script.

### Include JavaScript files on your page

[Section titled “Include JavaScript files on your page”](#include-javascript-files-on-your-page)

You may want to write your scripts as separate `.js`/`.ts` files or need to reference an external script on another server. You can do this by referencing these in a `<script>` tag’s `src` attribute.

#### Import local scripts

[Section titled “Import local scripts”](#import-local-scripts)

**When to use this:** when your script lives inside of `src/`.

Astro will process these scripts according to the [script processing rules](#script-processing).

#### Load external scripts

[Section titled “Load external scripts”](#load-external-scripts)

**When to use this:** when your JavaScript file lives inside of `public/` or on a CDN.

To load scripts outside of your project’s `src/` folder, include the `is:inline` directive. This approach skips the JavaScript processing, bundling, and optimizations that are provided by Astro when you import scripts as described above.

## Common script patterns

[Section titled “Common script patterns”](#common-script-patterns)

### Handle `onclick` and other events

[Section titled “Handle onclick and other events”](#handle-onclick-and-other-events)

Some UI frameworks use custom syntax for event handling like `onClick={...}` (React/Preact) or `@click="..."` (Vue). Astro follows standard HTML more closely and does not use custom syntax for events.

Instead, you can use [ addEventListener](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener) in a 

`<script>` tag to handle user interactions.If you have multiple `<AlertButton />` components on a page, Astro will not run the script multiple times. Scripts are bundled and only included once per page. Using `querySelectorAll` ensures that this script attaches the event listener to every button with the `alert` class found on the page.

### Web components with custom elements

[Section titled “Web components with custom elements”](#web-components-with-custom-elements)

You can create your own HTML elements with custom behavior using the Web Components standard. Defining a [custom element](https://developer.mozilla.org/en-US/docs/Web/Web_Components/Using_custom_elements) in a `.astro` component allows you to build interactive components without needing a UI framework library.

In this example, we define a new `<astro-heart>` HTML element that tracks how many times you click the heart button and updates the `<span>` with the latest count.

There are two advantages to using a custom element here:

- 
Instead of searching the whole page using `document.querySelector()`, you can use`this.querySelector()`, which only searches within the current custom element instance. This makes it easier to work with only the children of one component instance at a time.
- 
Although a `<script>`only runs once, the browser will run our custom element’s`connectedCallback()`method each time it finds`<astro-heart>`on the page. This means you can safely write code for one component at a time, even if you intend to use this component multiple times on a page.

[web.dev’s Reusable Web Components guide](https://web.dev/custom-elements-v1/)and

[MDN’s introduction to custom elements](https://developer.mozilla.org/en-US/docs/Web/Web_Components/Using_custom_elements).

### Pass frontmatter variables to scripts

[Section titled “Pass frontmatter variables to scripts”](#pass-frontmatter-variables-to-scripts)

In Astro components, the code in [the frontmatter](/en/basics/astro-components/#the-component-script) (between the `---` fences) runs on the server and is not available in the browser.

To pass server-side variables to client-side scripts, store them in [ data-* attributes](https://developer.mozilla.org/en-US/docs/Learn/HTML/Howto/Use_data_attributes) on HTML elements. Scripts can then access these values using the 

`dataset` property.In this example component, a `message` prop is stored in a `data-message` attribute, so the custom element can read `this.dataset.message` and get the value of the prop in the browser.

Now we can use our component multiple times and be greeted by a different message for each one.

This is actually what Astro does behind the scenes when you pass props to a component written using a UI framework like React! For components with a `client:*` directive, Astro creates an `<astro-island>` custom element with a `props` attribute that stores your server-side props in the HTML output.

### Combining scripts and UI Frameworks

[Section titled “Combining scripts and UI Frameworks”](#combining-scripts-and-ui-frameworks)

Elements rendered by a UI framework may not be available yet when a `<script>` tag executes. If your script also needs to handle [UI framework components](/en/guides/framework-components/), using a custom element is recommended.

[Contribute](/en/contribute/)

[Community](https://astro.build/chat)

[Sponsor](https://opencollective.com/astrodotbuild)

# Citations

1. Source page: https://docs.astro.build/en/guides/client-side-scripts
