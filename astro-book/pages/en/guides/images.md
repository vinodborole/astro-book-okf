---
type: Web Page
title: Images | Docs
description: Learn how to use images in Astro.
resource: https://docs.astro.build/en/guides/images
timestamp: '2026-08-03T09:35:37.104348+00:00'
---

# Images

Astro provides several ways for you to use images on your site, whether they are stored locally inside your project, linked to from an external URL, or managed in a CMS or CDN.

Astro provides built-in [`<Image />`](#image-) and [`<Picture />`](#picture-) Astro components, [Markdown image syntax](#images-in-markdown-files) (`![]()`) processing, [SVG components](#svg-components), and [an image generating function](#generating-images-with-getimage) to optimize and/or transform your images. Additionally, you can configure [automatically resizing responsive images](#responsive-image-behavior) by default, or set responsive properties on individual image and picture components.

You can always choose to use images and SVG files using native HTML elements in `.astro` or Markdown files, or the standard way for your file type (e.g. `<img />` in MDX and JSX). However, Astro does not perform any processing or optimization of these images.

There is also no native video support in Astro, and we recommend choosing a [hosted video service](/en/guides/media/) to handle the demands of optimizing and streaming video content.

[and](/en/reference/modules/astro-assets/#image-)

`<Image />`
[components.](/en/reference/modules/astro-assets/#picture-)

`<Picture />`
## Where to store images

[Section titled “Where to store images”](#where-to-store-images)

### `src/` vs `public/`

[Section titled “src/ vs public/”](#src-vs-public)

We recommend that local images are kept in `src/` when possible so that Astro can transform, optimize, and bundle them. Files in the `public/` directory are always served or copied into the build folder as-is, with no processing.

Your local images stored in `src/` can be used by all files in your project: `.astro`, `.md`, `.mdx`, `.mdoc`, and other UI frameworks as file imports. Images can be stored in any folder, including alongside your content.

Store your images in the `public/` folder if you want to avoid any processing. These images are available to your project files as URL paths on your domain and allow you to have a direct public link to them. For example, your site favicon will commonly be placed in the root of this folder where browsers can identify it.

### Remote images

[Section titled “Remote images”](#remote-images)

You can also choose to store your images remotely, in a [content management system (CMS)](/en/guides/cms/) or [digital asset management (DAM)](/en/guides/media/) platform. Astro can fetch your data remotely using APIs or display images from their full URL path.

For extra protection when dealing with external sources, Astro’s image components and helper function will only process (e.g. optimize, transform) images from [authorized image sources specified in your configuration](#authorizing-remote-images). Remote images from other sources will be displayed with no processing.

## Images in `.astro` files

[Section titled “Images in .astro files”](#images-in-astro-files)

**Options:** `<Image />`, `<Picture />`, `<img>`, `<svg>`, SVG components

Astro’s templating language allows you to render optimized images with the Astro [`<Image />`](/en/reference/modules/astro-assets/#image-) component and generate multiple sizes and formats with the Astro [`<Picture />`](/en/reference/modules/astro-assets/#picture-) component. Both components also accept [responsive image properties](#responsive-image-behavior) for resizing based on container size and responding to device screen size and resolution.

Additionally, you can import and use [SVG files as Astro components](#svg-components) in `.astro` components.

All native HTML tags, including `<img>` and `<svg>`, are also available in `.astro` components. [Images rendered with HTML tags](#display-unprocessed-images-with-the-html-img-tag) will not be processed (e.g. optimized, transformed) and will be copied into your build folder as-is.

For all images in `.astro` files, **the value of the image `src` attribute is determined by the location of your image file**:

- 
A local image from your project `src/` folder uses an import from the file’s relative path.The image and picture components use the named import directly (e.g. `src={rocket}` ), while the`<img>` tag uses the`src` object property of the import (e.g.`src={rocket.src}` ).
- 
Remote and `public/` images use a URL path.Provide a full URL for remote images (e.g. `src="https://www.example.com/images/my-remote-image.jpg"` ), or a relative URL path on your site that corresponds to your file’s location in your`public/` folder (e.g.`src="/images/my-public-image.jpg"` for an image located in`public/images/my-public-image.jpg` ).

[and](/en/reference/modules/astro-assets/#image-)

`<Image />`
[components including required and optional properties.](/en/reference/modules/astro-assets/#picture-)

`<Picture />`
**Related recipe:**

[Dynamically import images](/en/recipes/dynamically-importing-images/)

## Images in Markdown files

[Section titled “Images in Markdown files”](#images-in-markdown-files)

**Options:** `![]()`, `<img>` (with public or remote images)

Use standard Markdown `![alt](src)` syntax in your `.md` files. Your local images stored in `src/` and remote images will be processed and optimized. When you [configure responsive images globally](/en/reference/configuration-reference/#imagelayout), these images will also be [responsive](#responsive-image-behavior).

Images stored in the `public/` folder are never optimized.

The HTML `<img>` tag can also be used to display images stored in `public/` or remote images without any image optimization or processing. However, `<img>` is not supported for your local images in `src`.

The `<Image />` and `<Picture />` components are unavailable in `.md` files. If you require more control over your image attributes, we recommend using [Astro’s MDX integration](/en/guides/integrations-guide/mdx/) to add support for `.mdx` file format. MDX allows additional [image options available in MDX](#images-in-mdx-files), including combining components with Markdown syntax.

## Images in MDX files

[Section titled “Images in MDX files”](#images-in-mdx-files)

**Options:** `<Image />`, `<Picture />`, `<img />`, `![]()`, SVG components

You can use Astro’s `<Image />` and `<Picture />` components in your `.mdx` files by importing both the component and your image. Use them just as they are [used in `.astro` files](#images-in-astro-files). The JSX `<img />` tag is also supported for unprocessed images and [uses the same image import as the HTML `<img>` tag](#display-unprocessed-images-with-the-html-img-tag).

Additionally, there is support for [standard Markdown `!\[alt\](src)` syntax](#images-in-markdown-files) with no import required.

[and](/en/reference/modules/astro-assets/#image-)

`<Image />`
[components.](/en/reference/modules/astro-assets/#picture-)

`<Picture />`
## Images in UI framework components

[Section titled “Images in UI framework components”](#images-in-ui-framework-components)

**Image options:** the framework’s own image syntax (e.g. `<img />` in JSX, `<img>` in Svelte)

[Local images must first be imported](#display-unprocessed-images-with-the-html-img-tag) to access their image properties such as `src`. Then, they can be rendered as you normally would in that framework’s own image syntax:

Astro components (e.g. `<Image />`, `<Picture />`, SVG components) are unavailable inside UI framework components because [a client island must contain only valid code for its own framework](/en/guides/framework-components/#can-i-use-astro-components-inside-my-framework-components).

But, you can pass the static content generated by these components to a framework component inside a `.astro` file [as children](/en/guides/framework-components/#passing-children-to-framework-components) or using a [named `<slot/>`](/en/guides/framework-components/#can-i-use-astro-components-inside-my-framework-components):

## Astro components for images

[Section titled “Astro components for images”](#astro-components-for-images)

Astro provides two built-in Astro components for images (`<Image />` and `<Picture />`) and also allows you to import SVG files and use them as Astro components. These components may be used in any files that can import and render `.astro` components.

### `<Image />`

[Section titled “<Image />”](#image-)

Use the built-in `<Image />` Astro component to display optimized versions of:

- your local images located within the `src/` folder
- [configured remote images](#authorizing-remote-images) from authorized sources

`<Image />` can transform a local or authorized remote image’s dimensions, file type, and quality for control over your displayed image. This transformation happens at build time for prerendered pages. When your page is rendered on demand, this transformation will occur on the fly when the page is viewed. The resulting `<img>` tag includes `alt`, `loading`, and `decoding` attributes and infers image dimensions to avoid Cumulative Layout Shift (CLS).

[Cumulative Layout Shift (CLS)](https://web.dev/cls/) is a Core Web Vital metric for measuring how much content shifted on your page during loading. The `<Image />` component optimizes for CLS by automatically setting the correct `width` and `height` for your images.

The `<Image />` component accepts [several component properties](/en/reference/modules/astro-assets/#image-) as well as any attributes accepted by the HTML `<img>` tag.

The following example provides a `class` to the image component which will apply to the final `<img>` element.

You can also use the `<Image />` component for images in the `public/` folder, or remote images not specifically configured in your project, even though these images will not be optimized or processed. The resulting image will be the same as using the HTML `<img>`.

However, using the image component for all images provides a consistent authoring experience and prevents Cumulative Layout Shift (CLS) even for your unoptimized images.

### `<Picture />`

[Section titled “<Picture />”](#picture-)

	**Added in:**
	`astro@3.3.0`
	
	

Use the built-in `<Picture />` Astro component to generate a `<picture>` tag with multiple formats and/or sizes of your image. This allows you to specify preferred file formats to display and at the same time, provide a fallback format. Like the [`<Image />` component](#image-), images will be processed at build time for prerendered pages. When your page is rendered on demand, processing will occur on the fly when the page is viewed.

The following example uses the `<Picture />` component to transform a local `.png` file into a web-friendly `avif` and `webp` format as well as the `.png` `<img>` that can be displayed as a fallback when needed:

[the](/en/reference/modules/astro-assets/#picture-)in the

`<Picture />` component properties`astro:assets` reference.
### Responsive image behavior

[Section titled “Responsive image behavior”](#responsive-image-behavior)

	**Added in:**
	`astro@5.10.0`
	
	

Responsive images are images that adjust to improve performance across different devices. These images can resize to fit their container, and can be served in different sizes depending on your visitor’s screen size and resolution.

With the [layout property](/en/reference/modules/astro-assets/#layout) applied to the `<Image />` or `<Picture />` components, Astro will automatically generate the required `srcset` and `sizes` values for your images, and apply the necessary [styles to ensure they resize correctly](#responsive-image-styles).

When this responsive behavior is [configured globally with `image.layout`](/en/reference/configuration-reference/#imagelayout), it will apply to all image components and also to any local and remote images using [the Markdown `!\[\]()` syntax](/en/guides/images/#images-in-markdown-files).

Images in your `public/` folder are never optimized, and responsive images are not supported.

A single responsive image will generate multiple images of different sizes so that the browser can show the best one to your visitor.

For prerendered pages, this happens during the build and may increase the build time of your project, especially if you have a large number of images.

For pages rendered on-demand, the images are generated as-needed when a page is visited. This has no impact on build times but may increase the number of image transformations performed when an image is displayed. Depending on your image service this may incur additional costs.

[responsive images on MDN web docs](https://developer.mozilla.org/en-US/docs/Web/HTML/Guides/Responsive_images).

#### Generated HTML output for responsive images

[Section titled “Generated HTML output for responsive images”](#generated-html-output-for-responsive-images)

When a layout is set, either by default or on an individual component, images have automatically generated `srcset` and `sizes` attributes based on the image’s dimensions and the layout type. Images with `constrained` and `full-width` layouts will have styles applied to ensure they resize according to their container.

This `<Image />` component will generate the following HTML output on a prerendered page:

#### Responsive image styles

[Section titled “Responsive image styles”](#responsive-image-styles)

Setting [`image.responsiveStyles: true`](/en/reference/configuration-reference/#imageresponsivestyles) applies a small number of global styles to ensure that your images resize correctly. In most cases, you will want to enable these as a default; your images will not be responsive without additional styles.

However, if you prefer to handle responsive image styling yourself, or need to [override these defaults when using Tailwind 4](#responsive-images-with-tailwind-4), leave the default `false` value configured.

The global styles applied by Astro will depend on the layout type, and are designed to produce the best result for the generated `srcset` and `sizes` attributes. These are the default styles:

The styles use the [`:where()` pseudo-class](https://developer.mozilla.org/en-US/docs/Web/CSS/:where), which has a [specificity](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_cascade/Specificity) of 0, meaning that it is easy to override with your own styles. Any CSS selector will have a higher specificity than `:where()`, so you can easily override the styles by adding your own styles to target the image.

You can override the `object-fit` and `object-position` styles on a per-image basis by setting the `fit` and `position` props on the `<Image />` or `<Picture />` component.

#### Responsive images with Tailwind 4

[Section titled “Responsive images with Tailwind 4”](#responsive-images-with-tailwind-4)

Tailwind 4 is compatible with Astro’s default responsive styles. However, Tailwind uses [cascade layers](https://developer.mozilla.org/en-US/docs/Web/CSS/@layer), meaning that its rules are always lower specificity than rules that don’t use layers, including Astro’s responsive styles. Therefore, Astro’s styling will take precedence over Tailwind styling. To use Tailwind rules instead of Astro’s default styling, do not enable [Astro’s default responsive styles](/en/reference/configuration-reference/#imageresponsivestyles).

### SVG components

[Section titled “SVG components”](#svg-components)

	**Added in:**
	`astro@5.7.0`
	
	

Astro allows you to import SVG files and use them as Astro components. Astro will inline the SVG content into your HTML output.

Reference the default import of any local `.svg` file. Since this import is treated as an Astro component, you must use the same conventions (e.g. capitalization) as when [using dynamic tags](/en/reference/astro-syntax/#dynamic-tags).

Your SVG component, like `<Image />` or any other Astro component, is unavailable inside UI framework components, but can [be passed to a framework component](#images-in-ui-framework-components) inside a `.astro` component.

#### SVG component attributes

[Section titled “SVG component attributes”](#svg-component-attributes)

You can pass props such as `width`, `height`, `fill`, `stroke`, and any other attribute accepted by the [native `<svg>` element](https://developer.mozilla.org/en-US/docs/Web/SVG/Element/svg). These attributes will automatically be applied to the underlying `<svg>` element. If a property is present in the original `.svg` file and is passed to the component, the value passed to the component will override the original value.

#### `SvgComponent` Type

[Section titled “SvgComponent Type”](#svgcomponent-type)

**Added in:**

`astro@5.14.0`
	
	
You can also enforce type safety for your `.svg` assets using the `SvgComponent` type:

### Creating custom image components

[Section titled “Creating custom image components”](#creating-custom-image-components)

You can create a custom, reusable image component by wrapping the `<Image />`  or `<Picture/>` component in another Astro component. This allows you to set default attributes and styles only once.

For example, you could create a component for your blog post images that receives attributes as props and applies consistent styles to each image:

## Display unprocessed images with the HTML `<img>` tag

[Section titled “Display unprocessed images with the HTML <img> tag”](#display-unprocessed-images-with-the-html-img-tag)

The [Astro template syntax](/en/reference/astro-syntax/) also supports writing an `<img>` tag directly, with full control over its final output. These images will not be processed and optimized. It accepts all HTML `<img>` tag properties, and the only required property is `src`. However, it is strongly recommended to include [the `alt` property for accessibility](#alt-text).

### images in `src/`

[Section titled “images in src/”](#images-in-src)

Local images must be imported from the relative path from the existing `.astro` file, or you can configure and use an [import alias](/en/guides/imports/#aliases). Then, you can access the image’s `src` and other properties to use in the `<img>` tag.

Imported image assets match the [`ImageMetadata` type](/en/reference/modules/astro-assets/#imagemetadata-1) and have the following signature:

The following example uses the image’s own `height` and `width` properties to avoid Cumulative Layout Shift (CLS) and improve Core Web Vitals:

### Images in `public/`

[Section titled “Images in public/”](#images-in-public)

For images located within `public/` use the image’s file path relative to the public folder as the `src` value:

### Remote images

[Section titled “Remote images”](#remote-images-1)

For remote images, use the image’s full URL as the `src` value:

### Choosing `<Image />` vs `<img>`

[Section titled “Choosing <Image /> vs <img>”](#choosing-image--vs-img)

The `<Image />` component optimizes your image and infers width and height (for images it can process) based on the original aspect ratio to avoid CLS. It is the preferred way to use images in `.astro` files whenever possible.

Use the HTML `<img>` element when you cannot use the `<Image />` component, for example:

- for unsupported image formats
- when you do not want your image optimized by Astro
- to access and change the `src` attribute dynamically client-side

## Using Images from a CMS or CDN

[Section titled “Using Images from a CMS or CDN”](#using-images-from-a-cms-or-cdn)

Image CDNs work with [all Astro image options](#images-in-astro-files). Use an image’s full URL as the `src` attribute in the `<Image />` component, an `<img>` tag, or in Markdown notation. For image optimization with remote images, also [configure your authorized domains or URL patterns](#authorizing-remote-images).

Alternatively, the CDN may provide its own SDKs to more easily integrate in an Astro project. For example:

- Cloudinary supports an [Astro SDK](https://astro.cloudinary.dev/) which allows you to easily drop in images with their`CldImage` component or a[Node.js SDK](https://cloudinary.com/documentation/node_integration) that can generate URLs to use with an`<img>` tag in a Node.js environment.
- ImageKit provides an [Astro integration](https://github.com/imagekit-developer/imagekit-astro) that registers an image service. This means Astro’s built-in`<Image />` and`<Picture />` components, along with Markdown`![]()` and MDX images, are all routed through ImageKit automatically. It adds CDN delivery, automatic AVIF/WebP conversion, responsive`srcset` , and on-the-fly transformations without changing your existing image syntax.

[and](/en/reference/modules/astro-assets/#image-)

`<Image />`
[components.](/en/reference/modules/astro-assets/#picture-)

`<Picture />`
## Authorizing remote images

[Section titled “Authorizing remote images”](#authorizing-remote-images)

You can configure lists of authorized image source URL domains and patterns for image optimization using [`image.domains`](/en/reference/configuration-reference/#imagedomains) and [`image.remotePatterns`](/en/reference/configuration-reference/#imageremotepatterns). This configuration is an extra layer of safety to protect your site when showing images from an external source.

Remote images from other sources will not be optimized, but using the `<Image />` component for these images will prevent Cumulative Layout Shift (CLS).

For example, the following configuration will only allow remote images from `astro.build` to be optimized:

The following configuration will only allow remote images from HTTPS hosts:

## Images in content collections

[Section titled “Images in content collections”](#images-in-content-collections)

You can declare an associated image for a content collections entry, such as a blog post’s cover image, in your frontmatter using its path relative to the current folder:

The `image` helper for the content collections schema lets you validate and import the image.

The image will be imported and transformed into metadata, allowing you to pass it as a `src` to `<Image/>`, `<img>`, or `getImage()` in an Astro component.

The example below shows a blog index page that renders the cover photo and title of each blog post from the previous schema:

## Generating images with `getImage()`

[Section titled “Generating images with getImage()”](#generating-images-with-getimage)

The `getImage()` function is intended for generating images destined to be used somewhere else than directly in HTML, for example in an [API Route](/en/guides/endpoints/#server-endpoints-api-routes). When you need options that the `<Picture>` and `<Image>` components do not currently support, you can use the `getImage()` function to create your own custom `<Image />` component.

`getImage()` can only be used on the server. If you need to use the resulting image URL on the client (e.g. in a client-side script or framework component), call `getImage()` inside the frontmatter and pass the resulting `src` to the client:

[.](/en/reference/modules/astro-assets/#getimage)

`getImage()` reference
**Related recipe:**

[Build a custom image component](/en/recipes/build-custom-img-component/)

## Alt Text

[Section titled “Alt Text”](#alt-text)

Not all users can see images in the same way, so accessibility is an especially important concern when using images. Use the `alt` attribute to provide [descriptive alt text](https://www.w3.org/WAI/tutorials/images/) for images.

This attribute is required for both the `<Image />` and `<Picture />` components. If no alt text is provided, a helpful error message will be provided reminding you to include the `alt` attribute.

If the image is merely decorative (i.e. doesn’t contribute to the understanding of the page), set `alt=""` so that screen readers know to ignore the image.

## Default image service

[Section titled “Default image service”](#default-image-service)

[Sharp](https://github.com/lovell/sharp) is the default image service used for `astro:assets`. You can further configure the image service using the [`image.service`](/en/reference/configuration-reference/#imageservice) option.

When using a [strict package manager](https://pnpm.io/pnpm-vs-npm#npms-flat-tree) like `pnpm`, you may need to manually install Sharp into your project even though it is an Astro dependency:

### Configure no-op passthrough service

[Section titled “Configure no-op passthrough service”](#configure-no-op-passthrough-service)

If your [adapter](https://astro.build/integrations/?search=&categories%5B%5D=adapters) does not support Astro’s built-in Sharp image optimization (e.g. Cloudflare), you can configure a no-op image service to allow you to use the `<Image />` and `<Picture />` components. Note that Astro does not perform any image transformation and processing in these environments. However, you can still enjoy the other benefits of using `astro:assets`, including no Cumulative Layout Shift (CLS), the enforced `alt` attribute, and a consistent authoring experience.

Configure the `passthroughImageService()` to avoid Sharp image processing:

## Asset Caching

[Section titled “Asset Caching”](#asset-caching)

Astro stores processed image assets in a cache directory during site builds for both local and [remote images from authorized sources](#authorizing-remote-images). By preserving the cache directory between builds, processed assets are reused, improving build time and bandwidth usage.

The default cache directory is `./node_modules/.astro`, however this can be changed using the [`cacheDir`](/en/reference/configuration-reference/#cachedir) configuration setting.

### Remote Images

[Section titled “Remote Images”](#remote-images-2)

Remote images in the asset cache are managed based on [HTTP Caching](https://developer.mozilla.org/en-US/docs/Web/HTTP/Caching), and respect the [Cache-Control header](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control) returned by the remote server.
Images are cached if the Cache-Control header allows, and will be used until they are no longer [fresh](https://developer.mozilla.org/en-US/docs/Web/HTTP/Caching#fresh_and_stale_based_on_age).

#### Revalidation

[Section titled “Revalidation”](#revalidation)

	**Added in:**
	`astro@5.1.0`
	
	

[Revalidation](https://developer.mozilla.org/en-US/docs/Web/HTTP/Caching#validation) reduces bandwidth usage and build time by checking with the remote server whether an expired cached image is still up-to-date. If the server indicates that the image is still fresh, the cached version is reused, otherwise the image is redownloaded.

Revalidation requires that the remote server send [Last-Modified](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Last-Modified) and/or [Etag (entity tag)](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/ETag) headers with its responses. This feature is available for remote servers that support the [If-Modified-Since](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/If-Modified-Since) and [If-None-Match](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/If-None-Match) headers.

## Community Integrations

[Section titled “Community Integrations”](#community-integrations)

There are several third-party [community image integrations](https://astro.build/integrations?search=images) for optimizing and working with images in your Astro project.

[Contribute](/en/contribute/)

[Community](https://astro.build/chat)

[Sponsor](https://opencollective.com/astrodotbuild)

# Citations

1. Source page: https://docs.astro.build/en/guides/images
