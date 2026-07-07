---
type: Web Page
title: Build forms with API routes | Docs
description: Learn how to use JavaScript to send form submissions to an API Route.
resource: https://docs.astro.build/en/recipes/build-forms-api
timestamp: '2026-07-07T10:59:34.007706+00:00'
---

# Build forms with API routes

An HTML form causes the browser to refresh the page or navigate to a new one. To send form data to an API endpoint instead, you must intercept the form submission using JavaScript.

This recipe shows you how to send form data to an API endpoint and handle that data.

## Prerequisites

Section titled “Prerequisites”- A project with an adapter for on-demand rendering
- A UI Framework integration installed

## Recipe

Section titled “Recipe”- 
Create a `POST`API endpoint at`/api/feedback`that will receive the form data. Use`request.formData()`to process it. Be sure to validate the form values before you use them.This example sends a JSON object with a message back to the client. 
- 
Create a form component using your UI framework. Each input should have a `name`attribute that describes the value of that input.Be sure to include a `<button>`or`<input type="submit">`element to submit the form.
- 
Create a function that accepts a submit event, then pass it as a `submit`handler to your form.In the function: - Call `preventDefault()`on the event to override the browser’s default submission process.
- Create a `FormData`object and send it in a`POST`request to your endpoint using`fetch()`.
 
- Call 
- 
Import and include your `<FeedbackForm />`component on a page. Be sure to use a`client:*`directive to ensure that the form logic is hydrated when you want it to be.

# Citations

1. Source page: https://docs.astro.build/en/recipes/build-forms-api
