---
type: Web Page
title: Verify a Captcha | Docs
description: Learn how to create an API route and fetch it from the client.
resource: https://docs.astro.build/en/recipes/captcha
timestamp: '2026-08-03T09:35:37.104348+00:00'
---

# Verify a Captcha

[Server endpoints](/en/guides/endpoints/#server-endpoints-api-routes) can be used as REST API endpoints to run functions such as authentications, database access, and verifications without exposing sensitive data to the client.

In this recipe, an API route is used to verify Google reCAPTCHA v3 without exposing the secret to clients.

## Prerequisites

[Section titled “Prerequisites”](#prerequisites)

- A project with [SSR](/en/guides/on-demand-rendering/) (`output: 'server'` ) enabled

## Recipe

[Section titled “Recipe”](#recipe)

1. 
Create a `POST` endpoint that accepts recaptcha data, then verifies it with reCAPTCHA’s API. Here, you can safely define secret values or read environment variables.
2. 
Access your endpoint using `fetch` from a client script:

[Contribute](/en/contribute/)

[Community](https://astro.build/chat)

[Sponsor](https://opencollective.com/astrodotbuild)

# Citations

1. Source page: https://docs.astro.build/en/recipes/captcha
