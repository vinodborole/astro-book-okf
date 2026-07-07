---
type: Web Page
title: Share state between Astro components | Docs
description: Learn how to share state across Astro components with Nano Stores.
resource: https://docs.astro.build/en/recipes/sharing-state
timestamp: '2026-07-07T10:59:34.007706+00:00'
---

# Share state between Astro components

Using framework components? See how to share state between Islands!

When building an Astro website, you may need to share state across components. Astro recommends the use of Nano Stores for shared client storage.

## Recipe

Section titled “Recipe”- 
Install Nano Stores: 
- 
Create a store. In this example, the store tracks whether a dialog is open or not: 
- 
Import and use the store in a `<script>`tag in the components that will share state.The following `Button`and`Dialog`components each use the shared`isOpen`state to control whether a particular`<div>`is hidden or displayed:

# Citations

1. Source page: https://docs.astro.build/en/recipes/sharing-state
