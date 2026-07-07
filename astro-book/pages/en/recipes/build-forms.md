---
type: Web Page
title: Build HTML forms in Astro pages | Docs
description: Learn how to build HTML forms and handle submissions in your frontmatter.
resource: https://docs.astro.build/en/recipes/build-forms
timestamp: '2026-07-07T10:59:34.007706+00:00'
---

# Build HTML forms in Astro pages

Astro pages that are rendered on demand can both display and handle forms. In this recipe, you’ll use a standard HTML form to submit data to the server. Your frontmatter script will handle the data on the server, sending no JavaScript to the client.

In v4.15, Astro added actions which provide several benefits over basic HTML forms including validating your form data and updating your UI based on the form submission. To use this method for building forms instead, see our actions guide to learn more about these features.

## Prerequisites

Section titled “Prerequisites”- An Astro project with a server adapter installed.

## Recipe

Section titled “Recipe”- 
Create or identify a `.astro`page which will contain your form and your handling code. For example, you could add a registration page:
- 
Add a `<form>`tag with some inputs to the page. Each input should have a`name`attribute that describes the value of that input.Be sure to include a `<button>`or`<input type="submit">`element to submit the form.
- 
Use validation attributes to provide basic client-side validation that works even if JavaScript is disabled. In this example, - `required`prevents form submission until the field is filled.
- `minlength`sets a minimum required length for the input text.
- `type="email"`also introduces validation that will only accept a valid email format.
 You can add custom validation logic that refers to multiple fields using a `<script>`tag and the Constraint Validation API.To write complex validation logic more easily, you can build your form using a frontend framework and choose a form library like React Hook Form or Felte. 
- 
The form submission will cause the browser to request the page again. Change the form’s data transfer `method`to`POST`to send the form data as part of the`Request`body, rather than as URL parameters.
- 
Check for the `POST`method in the frontmatter and access the form data using`Astro.request.formData()`. Wrap this in a`try ... catch`block to handle cases when the`POST`request wasn’t sent by a form and the`formData`is invalid.
- 
Validate the form data on the server. This should include the same validation done on the client to prevent malicious submissions to your endpoint and to support the rare legacy browser that doesn’t have form validation. It can also include validation that can’t be done on the client. For example, this example checks if the email is already in the database. Error messages can be sent back to the client by storing them in an `errors`object and accessing it in the template.

# Citations

1. Source page: https://docs.astro.build/en/recipes/build-forms
