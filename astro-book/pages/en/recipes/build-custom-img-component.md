---
type: Web Page
title: Build a custom image component | Docs
description: Learn how to build a custom image component that supports media queries
  using the getImage function.
resource: https://docs.astro.build/en/recipes/build-custom-img-component
timestamp: '2026-08-03T09:35:37.104348+00:00'
---

# Build a custom image component

Astro provides two built-in components that you can use to display and optimize your images.  The `<Picture>` component allows you to display responsive images and work with different formats and sizes. The `<Image>` component will optimize your images and allow you to pass in different formats and quality properties.

When you need options that the `<Picture>` and `<Image>` components do not currently support, you can use the `getImage()` function to create a custom component.

In this recipe, you will use the [`getImage()` function](/en/guides/images/#generating-images-with-getimage) to create your own custom image component that displays different source images based on media queries.

## Recipe

[Section titled “Recipe”](#recipe)

1. 
Create a new Astro component and import the `getImage()` function
2. 
Create a new component for your custom image. `MyCustomComponent.astro` will receive three`props` from`Astro.props` . The`mobileImgUrl` and`desktopImgUrl` props are used for creating your image at different viewport sizes. The`alt` prop is used for the image’s alt text. These props will be passed wherever you render your custom image components. Add the following imports and define the props that you will use in your component. You can also use TypeScript to type the props.
3. 
Define each of your responsive images by calling the `getImage()` function with your desired properties.
4. 
Create a `<picture>` element that generates a`srcset` with your different images based on your desired media queries.
5. 
Import and use `<MyCustomImageComponent />` in any`.astro` file. Be sure to pass the necessary props for generating two different images at the different viewport sizes:

[Contribute](/en/contribute/)

[Community](https://astro.build/chat)

[Sponsor](https://opencollective.com/astrodotbuild)

# Citations

1. Source page: https://docs.astro.build/en/recipes/build-custom-img-component
