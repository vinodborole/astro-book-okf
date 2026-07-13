---
type: Web Page
title: Build your Astro site with Docker | Docs
description: Learn how to build your Astro site using Docker.
resource: https://docs.astro.build/en/recipes/docker
timestamp: '2026-07-13T09:18:12.222139+00:00'
---

# Build your Astro site with Docker

[Docker](https://docker.com) is a tool to build, deploy, and run applications using containers.

Docker images and containers can be deployed to many different platforms, like AWS, Azure, and [Google Cloud](/en/guides/deploy/google-cloud/#cloud-run-ssr-and-static). This recipe won’t cover how to deploy your site to a specific platform but will show you how to set up Docker for your project.

## Prerequisites

[Section titled “Prerequisites”](#prerequisites)

- Docker installed on your local machine. You can find [installation instructions for your operating system here](https://docs.docker.com/get-docker/).
- A Dockerfile in your project. You can [learn more about Dockerfiles here](https://docs.docker.com/engine/reference/builder/)and use the Dockerfiles in the following section as a starting point.

## Creating a Dockerfile

[Section titled “Creating a Dockerfile”](#creating-a-dockerfile)

Create a file called `Dockerfile` in your project’s root directory. This file contains the instructions to build your site, which will differ depending on your needs. This guide can’t show all possible options but will give you starting points for SSR and static mode.

If you’re using another package manager than npm, you’ll need to adjust the commands accordingly.

This Dockerfile will build your site and serve it using Node.js on port `4321` and therefore requires the [Node adapter](/en/guides/integrations-guide/node/) installed in your Astro project.

These are just examples of Dockerfiles. You can customize them to your needs. For example, you could use another image, like `node:lts-alpine`:

### Adding a .dockerignore

[Section titled “Adding a .dockerignore”](#adding-a-dockerignore)

Adding a `.dockerignore` file to your project is best practice. This file describes which files or folders should be ignored in the Docker `COPY` or `ADD` commands, very similar to how `.gitignore` works. This speeds up the build process and reduces the size of the final image.

This file should go in the same directory as the `Dockerfile` itself. [Read the  .dockerignore documentation for extra info](https://docs.docker.com/engine/reference/builder/#dockerignore-file)

### Static

[Section titled “Static”](#static)

#### Apache (httpd)

[Section titled “Apache (httpd)”](#apache-httpd)

The following Dockerfile will build your site and serve it using Apache httpd on port `80` with the default configuration.

Use this approach for simple websites that don’t need any special configuration. For more complex websites, it is recommended to use a custom configuration, either in Apache or NGINX.

In order to build the Dockerfile above, you’ll also need to create a configuration file for NGINX. Create a folder called `nginx` in your project’s root directory and create a file called `nginx.conf` inside.

### Multi-stage build (using SSR)

[Section titled “Multi-stage build (using SSR)”](#multi-stage-build-using-ssr)

Here’s an example of a more advanced Dockerfile that, thanks to Docker’s [multi-stage builds](https://docs.docker.com/build/building/multi-stage/), optimizes the build process for your site by not reinstalling the npm dependencies when only the source code changes. This can reduce the build time even by minutes, depending on the size of your dependencies.

## Recipe

[Section titled “Recipe”](#recipe)

- 
Build your container by running the following command in your project’s root directory. Use any name for `<your-astro-image-name>`:This will output an image, which you can run locally or deploy to a platform of your choice. 
- 
To run your image as a local container, use the following command. Replace `<local-port>`with an open port on your machine. Replace`<container-port>`with the port exposed by your Docker container (`4321`,`80`, or`8080`in the above examples.)You should be able to access your site at `http://localhost:<local-port>`.
- 
Now that your website is successfully built and packaged in a container, you can deploy it to a cloud provider. See the [Google Cloud](/en/guides/deploy/google-cloud/#cloud-run-ssr-and-static)deployment guide for one example, and the[Deploy your app](https://docs.docker.com/language/nodejs/deploy/)page in the Docker docs.

[Contribute](/en/contribute/)

[Community](https://astro.build/chat)

[Sponsor](https://opencollective.com/astrodotbuild)

# Citations

1. Source page: https://docs.astro.build/en/recipes/docker
