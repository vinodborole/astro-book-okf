---
type: Web Page
title: Share state between islands | Docs
description: Learn how to share state across framework components with Nano Stores.
resource: https://docs.astro.build/en/recipes/sharing-state-islands
timestamp: '2026-07-07T10:59:34.007706+00:00'
---

# Share state between islands

When building an Astro website with islands architecture / partial hydration, you may have run into this problem: **I want to share state between my components.**

UI frameworks like React or Vue may encourage “context” providers for other components to consume. But when partially hydrating components within Astro or Markdown, you can’t use these context wrappers.

Astro recommends a different solution for shared client-side storage: **Nano Stores**.

**Related recipe:**Share state between Astro components

## Why Nano Stores?

Section titled “Why Nano Stores?”The Nano Stores library allows you to author stores that any component can interact with. We recommend Nano Stores because:

- **They’re lightweight.**Nano Stores ship the bare minimum JS you’ll need (less than 1 KB) with zero dependencies.
- **They’re framework-agnostic.**This means sharing state between frameworks will be seamless! Astro is built on flexibility, so we love solutions that offer a similar developer experience no matter your preference.

Still, there are a number of alternatives you can explore. These include:

- Svelte’s built-in stores
- Solid signals outside of a component context
- Vue’s reactivity API
- Sending custom browser events between components

**🙋 Can I use Nano Stores in **`.astro` files or other server-side components?

`.astro` files or other server-side components?Nano Stores can be used in `<script>` tags to share state between `.astro` components. However, Using Nano Stores in the frontmatter of server-side components is not recommended because of the following restrictions:

- Writing to a store from a `.astro`file or non-hydrated component will*not*affect the value received by client-side components.
- You cannot pass a Nano Store as a “prop” to client-side components.
- You cannot subscribe to store changes from a `.astro`file, since Astro components do not re-render.

If you understand these restrictions and still find a use case, you can give Nano Stores a try! Just remember that Nano Stores are built for reactivity to changes on the **client** specifically.

**🙋 How do Svelte stores compare to Nano Stores?**

**Nano Stores and Svelte stores are very similar!** In fact, nanostores allow you to use the same `$` shortcut for subscriptions that you might use with Svelte stores.

If you want to avoid third-party libraries, Svelte stores are a great cross-island communication tool on their own. Still, you might prefer Nano Stores if a) you like their add-ons for “objects” and async state, or b) you want to communicate between Svelte and other UI frameworks like Preact or Vue.

**🙋 How do Solid signals compare to Nano Stores?**

If you’ve used Solid for a while, you may have tried moving signals or stores outside of your components. This is a great way to share state between Solid islands! Try exporting signals from a shared file:

…and all components importing `sharedCount` will share the same state. Though this works well, you might prefer Nano Stores if a) you like their add-ons for “objects” and async state, or b) you want to communicate between Solid and other UI frameworks like Preact or Vue.

## Installing Nano Stores

Section titled “Installing Nano Stores”To get started, install Nano Stores alongside their helper package for your favorite UI framework:

No helper package here! Nano Stores can be used like standard Svelte stores.

You can jump into the Nano Stores usage guide from here, or follow along with our example below!

## Usage example - ecommerce cart flyout

Section titled “Usage example - ecommerce cart flyout”Let’s say we’re building a simple ecommerce interface with three interactive elements:

- An “add to cart” submission form
- A cart flyout to display those added items
- A cart flyout toggle

**Try the completed example** on your machine or online via StackBlitz.

Your base Astro file may look like this:

### Using “atoms”

Section titled “Using “atoms””Let’s start by opening our `CartFlyout` whenever `CartFlyoutToggle` is clicked.

First, create a new JS or TS file to contain our store. We’ll use an “atom” for this:

Now, we can import this store into any file that needs to read or write. We’ll start by wiring up our `CartFlyoutToggle`:

Then, we can read `isCartOpen` from our `CartFlyout` component:

### Using “maps”

Section titled “Using “maps””**Maps are a great choice for objects you write to regularly!** Alongside the standard `get()` and `set()` helpers an `atom` provides, you’ll also have a `.setKey()` function to efficiently update individual object keys.

Now, let’s keep track of the items inside your cart. To avoid duplicates and keep track of “quantity,” we can store your cart as an object with the item’s ID as a key. We’ll use a Map for this.

Let’s add a `cartItem` store to our `cartStore.js` from earlier. You can also switch to a TypeScript file to define the shape if you’re so inclined.

Now, let’s export an `addCartItem` helper for our components to use.

- **If that item doesn’t exist in your cart**, add the item with a starting quantity of 1.
- **If that item**, bump the quantity by 1.- *does*already exist

**🙋 Why use **`.get()` here instead of a `useStore` helper?

`.get()` here instead of a `useStore` helper?You may have noticed we’re calling `cartItems.get()` here, instead of grabbing that `useStore` helper from our React / Preact / Solid / Vue examples. This is because **useStore is meant to trigger component re-renders.** In other words, `useStore` should be used whenever the store value is being rendered to the UI. Since we’re reading the value when an **event** is triggered (`addToCart` in this case), and we aren’t trying to render that value, we don’t need `useStore` here.

With our store in place, we can call this function inside our `AddToCartForm` whenever that form is submitted. We’ll also open the cart flyout so you can see a full cart summary.

Finally, we’ll render those cart items inside our `CartFlyout`:

Now, you should have a fully interactive ecommerce example with the smallest JS bundle in the galaxy 🚀

**Try the completed example** on your machine or online via StackBlitz!

# Citations

1. Source page: https://docs.astro.build/en/recipes/sharing-state-islands
