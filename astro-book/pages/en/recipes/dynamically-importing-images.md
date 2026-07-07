---
type: Web Page
title: Dynamically import images | Docs
description: Learn how to dynamically import images using Vite's import.meta.glob
  function.
resource: https://docs.astro.build/en/recipes/dynamically-importing-images
timestamp: '2026-07-07T10:59:34.007706+00:00'
---

# Dynamically import images

Local images must be imported into `.astro` files in order to display them. There will be times where you will want or need to dynamically import the image paths of your images instead of explicitly importing each individual image.

In this recipe, you will learn how to dynamically import your images using Vite’s `import.meta.glob` function. You will build a card component that displays the name, age, and photo of a person.

## Recipe

Section titled “Recipe”- 
Create a new `assets`folder under the`src`directory and add your images inside that new folder.- ## Directorysrc/- ## Directoryassets/- avatar-1.jpg
- avatar-2.png
- avatar-3.jpeg
 
 
 `assets`is a popular folder name convention for placing images but you are free to name the folder whatever you like.
- 
Create a new Astro component for your card and import the `<Image />`component.
- 
Specify the `props`that your component will receive in order to display the necessary information on each card. You can optionally define their types, if you are using TypeScript in your project.
- 
Create a new `images`variable and use the`import.meta.glob`function which returns an object of all of the image paths inside the`assets`folder. You will also need to import`ImageMetadata`type to help define the type of the`images`variable.
- 
Use the props to create the markup for your card component. 
- 
Inside the `src`attribute, pass in the`images`object and use bracket notation for the image path. Then make sure to invoke the glob function.Since you are accessing the `images`object which has an unknown type, you should also`throw`an error in case an invalid file path is passed as a prop.`images`is an object that contains all of the image paths inside the`assets`folder.The `imagePath`prop is a string that contains the path to the image that you want to display. The`import.meta.glob()`is doing the work of finding the image path that matches the`imagePath`prop and handling the import for you.
- 
Import and use the card component inside an Astro page, passing in the values for the `props`.

# Citations

1. Source page: https://docs.astro.build/en/recipes/dynamically-importing-images
