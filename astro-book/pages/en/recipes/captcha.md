---
type: Web Page
title: Verify a Captcha | Docs
description: Learn how to create an API route and fetch it from the client.
resource: https://docs.astro.build/en/recipes/captcha
timestamp: '2026-07-07T10:59:34.007706+00:00'
---

# Verify a Captcha

Server endpoints can be used as REST API endpoints to run functions such as authentications, database access, and verifications without exposing sensitive data to the client.

In this recipe, an API route is used to verify Google reCAPTCHA v3 without exposing the secret to clients.

## Prerequisites

Section titled “Prerequisites”- A project with SSR (`output: 'server'`) enabled

## Recipe

Section titled “Recipe”- 
Create a `POST`endpoint that accepts recaptcha data, then verifies it with reCAPTCHA’s API. Here, you can safely define secret values or read environment variables.
- 
Access your endpoint using `fetch`from a client script:

# Citations

1. Source page: https://docs.astro.build/en/recipes/captcha
