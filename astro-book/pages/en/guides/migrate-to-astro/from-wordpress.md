---
type: Web Page
title: Migrating from WordPress | Docs
description: Tips for migrating an existing WordPress project to Astro
resource: https://docs.astro.build/en/guides/migrate-to-astro/from-wordpress
timestamp: '2026-07-07T10:59:34.007706+00:00'
---

# Migrating from WordPress

WordPress is an open-source, personal publishing system built on PHP and MySQL.

You can use WordPress as a headless CMS for your Astro project. Follow our guide to use your existing WordPress content in a new Astro project.

## Key Similarities between WordPress and Astro

Section titled “Key Similarities between WordPress and Astro”WordPress and Astro share some similarities that will help you migrate your project:

- 
Both WordPress and Astro are ideal for content-driven websites like blogs and support writing your content in Markdown (requires a plugin in WordPress). Although the process for adding new content is different, writing in Markdown files for your Astro blog should feel familiar if you have used Markdown syntax in your WordPress editor. 
- 
Both WordPress and Astro encourage you to think about the design of your site in “blocks” (components). In Astro you will probably write more of your own code to create these blocks rather than rely on pre-built plugins. But thinking about the individual pieces of your site and how they are presented on the page should feel familiar. 

## Key Differences between WordPress and Astro

Section titled “Key Differences between WordPress and Astro”When you rebuild your WordPress site in Astro, you will notice some important differences:

- 
A WordPress site is edited using an online dashboard. In Astro, you will use a code editor and development environment to maintain your site. You can develop locally on your machine, or choose a cloud editor/development environment like StackBlitz or CodeSandbox. 
- 
WordPress has an extensive plugin and theme market. In Astro, you will find some themes and integrations available, but you may now have to build many of your existing features yourself instead of looking for third-party solutions. Or, you can choose to start with an Astro theme with built-in features! 
- 
WordPress stores your content in a database. In Astro, you will have individual files (typically Markdown or MDX) in your project directory for each page’s content. Or, you can choose to use a CMS for your content, even your existing WordPress site, and use Astro to fetch and present the data. 

## Switch from WordPress to Astro

Section titled “Switch from WordPress to Astro”To convert a WordPress blog to Astro, start with our blog theme starter template, or explore more community blog themes in our theme showcase.

You can pass a `--template` argument to the `create astro` command to start a new Astro project with one of our official starters. Or, you can start a new project from any existing Astro repository on GitHub.

You can continue to use your existing WordPress blog as your CMS for Astro, which means you will keep using your WordPress dashboard for writing your posts. Your content will be managed at WordPress, but all other aspects of your Astro site will be built in your code editing environment, and you will deploy your Astro site separately from your WordPress site. (Be sure to update your domain at your host to keep the same website URL!)

You may wish to take Astro’s Build a Blog Tutorial if you are new to working in a code editor and using GitHub to store and deploy your site. It will walk you through all the accounts and setup you need! You will also learn how to build Astro components yourself, and it will show you how to add blog posts directly in Astro if you choose not to use WordPress to write your content.

If you want to move all of your existing post content to Astro, you may find this tool for exporting Markdown from WordPress helpful. You may need to make some adjustments to the result if you have to convert a large or complicated WordPress site to Markdown.

To convert other types of sites, such as a portfolio or documentation site, see more official starter templates on astro.new. You’ll find a link to each project’s GitHub repository, as well as one-click links to open a working project in StackBlitz and CodeSandbox online development environments.

## Community Resources

Section titled “Community Resources”If you found (or made!) a helpful video or blog post about converting a WordPress site to Astro, add it to this list!

# Citations

1. Source page: https://docs.astro.build/en/guides/migrate-to-astro/from-wordpress
