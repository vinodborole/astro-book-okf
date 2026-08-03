---
type: Web Page
title: Actions | Docs
description: Learn how to create type-safe server functions you can call from anywhere.
resource: https://docs.astro.build/en/guides/actions
timestamp: '2026-08-03T09:35:37.104348+00:00'
---

# Actions

	**Added in:**
	`astro@4.15`
	
	

Astro Actions allow you to define and call backend functions with type-safety. Actions perform data fetching, JSON parsing, and input validation for you. This can greatly reduce the amount of boilerplate needed compared to using an [API endpoint](/en/guides/endpoints/).

Use actions instead of API endpoints for seamless communication between your client and server code and to:

- Automatically validate JSON and form data inputs using [Zod validation](/en/reference/modules/astro-zod/) .
- Generate type-safe functions to call your backend from the client and even [from HTML form actions](#call-actions-from-an-html-form-action) . No need for manual`fetch()` calls.
- Standardize backend errors with the [`ActionError`](/en/reference/modules/astro-actions/#actionerror) object.

## Basic usage

[Section titled “Basic usage”](#basic-usage)

Actions are defined in a `server` object exported from `src/actions/index.ts`:

Your actions are available as functions from the `astro:actions` module. Import `actions` and call them client-side within a [UI framework component](/en/guides/framework-components/), [a form POST request](#call-actions-from-an-html-form-action), or by using a `<script>` tag in an Astro component.

When you call an action, it returns an object with either `data` containing the JSON-serialized result, or `error` containing thrown errors.

### Write your first action

[Section titled “Write your first action”](#write-your-first-action)

Follow these steps to define an action and call it in a `script` tag in your Astro page.

1. 
Create a `src/actions/index.ts` file and export a`server` object.
2. 
Import the `defineAction()` utility from`astro:actions` , and the`z` object from`astro/zod` .
3. 
Use the `defineAction()` utility to define a`getGreeting` action. The`input` property will be used to validate input parameters with a[Zod schema](/en/reference/modules/astro-zod/#common-data-type-validators) and the`handler()` function includes the backend logic to run on the server.
4. 
Create an Astro component with a button that will fetch a greeting using your `getGreeting` action when clicked.
5. 
To use your action, import `actions` from`astro:actions` and then call`actions.getGreeting()` in the click handler. The`name` option will be sent to your action’s`handler()` on the server and, if there are no errors, the result will be available as the`data` property.

[and its properties.](/en/reference/modules/astro-actions/#defineaction)

`defineAction()`
## Organizing actions

[Section titled “Organizing actions”](#organizing-actions)

All actions in your project must be exported from the `server` object in the `src/actions/index.ts` file. You can define actions inline or you can move action definitions to separate files and import them. You can even group related functions in nested objects.

For example, to colocate all of your user actions, you can create a `src/actions/user.ts` file and nest the definitions of both `getUser` and `createUser` inside a single `user` object.

Then, you can import this `user` object into your `src/actions/index.ts` file and add it as a top-level key to the `server` object alongside any other actions:

Now, all of your user actions are callable from the `actions.user` object:

- `actions.user.getUser()`
- `actions.user.createUser()`

## Handling returned data

[Section titled “Handling returned data”](#handling-returned-data)

Actions return an object containing either `data` with the type-safe return value of your `handler()`, or an `error` with any backend errors. Errors may come from validation errors on the `input` property or thrown errors within the `handler()`.

Actions return a custom data format that can handle Dates, Maps, Sets, and URLs [using the Devalue library](https://github.com/Rich-Harris/devalue). Therefore, you can’t easily inspect the response from the network like you can with regular JSON. For debugging, you can instead inspect the `data` object returned by actions.

[See the](/en/reference/modules/astro-actions/#handler-property)for full details.

`handler()` API reference
### Checking for errors

[Section titled “Checking for errors”](#checking-for-errors)

It’s best to check if an `error` is present before using the `data` property. This allows you to handle errors in advance and ensures `data` is defined without an `undefined` check.

### Accessing `data` directly without an error check

[Section titled “Accessing data directly without an error check”](#accessing-data-directly-without-an-error-check)

To skip error handling, for example while prototyping or using a library that will catch errors for you, use the `.orThrow()` property on your action call to throw errors instead of returning an `error`. This will return the action’s `data` directly.

This example calls a `likePost()` action that returns the updated number of likes as a `number` from the action `handler`:

### Handling backend errors in your action

[Section titled “Handling backend errors in your action”](#handling-backend-errors-in-your-action)

You can use the provided `ActionError` to throw an error from your action `handler()`, such as “not found” when a database entry is missing, or “unauthorized” when a user is not logged in. This has two main benefits over returning `undefined`:

- 
You can set a status code like `404 - Not found` or`401 - Unauthorized` . This improves debugging errors in both development and in production by letting you see the status code of each request.
- 
In your application code, all errors are passed to the `error` object on an action result. This avoids the need for`undefined` checks on data, and allows you to display targeted feedback to the user depending on what went wrong.

#### Creating an `ActionError`

[Section titled “Creating an ActionError”](#creating-an-actionerror)

To throw an error, import the [`ActionError()` class](/en/reference/modules/astro-actions/#actionerror) from the `astro:actions` module. Pass it a human-readable status `code` (e.g. `"NOT_FOUND"` or `"BAD_REQUEST"`), and an optional `message` to provide further information about the error.

This example throws an error from a `likePost` action when a user is not logged in, after checking a hypothetical “user-session” cookie for authentication:

#### Handling an `ActionError`

[Section titled “Handling an ActionError”](#handling-an-actionerror)

To handle this error, you can call the action from your application and check whether an `error` property is present. This property will be of type `ActionError` and will contain your `code` and `message`.

In the following example, a `LikeButton.tsx` component calls the `likePost()` action when clicked. If an authentication error occurs, the `error.code` attribute is used to determine whether to display a login link:

### Handling client redirects

[Section titled “Handling client redirects”](#handling-client-redirects)

When calling actions from the client, you can integrate with a client-side library like `react-router`, or you can use Astro’s [`navigate()` function](/en/guides/view-transitions/#trigger-navigation) to redirect to a new page when an action succeeds.

This example navigates to the homepage after a `logout` action returns successfully:

## Accepting form data from an action

[Section titled “Accepting form data from an action”](#accepting-form-data-from-an-action)

Actions accept JSON data by default. To accept form data from an HTML form, set `accept: 'form'` in your `defineAction()` call:

### Using validators with form inputs

[Section titled “Using validators with form inputs”](#using-validators-with-form-inputs)

When your action is [configured to accept form data](/en/reference/modules/astro-actions/#accept-property), you can use any Zod validators to validate your fields (e.g. `z.coerce.date()` for date inputs). Extension functions including `.refine()`, `.transform()`, and `.pipe()` are also supported on the `z.object()` validator.

Additionally, Astro provides special handling under the hood for your convenience to validate the following types of field inputs:

- Inputs of type `number` can be validated using`z.number()`
- Inputs of type `checkbox` can be validated using`z.coerce.boolean()`
- Inputs of type `file` can be validated using`z.instanceof(File)`
- Multiple inputs of the same `name` can be validated using`z.array(/* validator */)`
- All other inputs can be validated using `z.string()`

When your form is submitted with empty inputs, the output type may not match your `input` validator. Empty values are converted to `null` except when validating arrays or booleans. For example, if an input of type `text` is submitted with an empty value, the result will be `null` instead of an empty string (`""`).

To apply a union of different validators, use the `z.discriminatedUnion()` wrapper to narrow the type based on a specific form field. This example accepts a form submission to either “create” or “update” a user, using the form field with the name `type` to determine which object to validate against:

### Validating form data

[Section titled “Validating form data”](#validating-form-data)

Actions will parse submitted form data to an object, using the value of each input’s `name` attribute as the object keys. For example, a form containing `<input name="search">` will be parsed to an object like `{ search: 'user input' }`. Your action’s `input` schema will be used to validate this object.

To receive the raw `FormData` object in your action handler instead of a parsed object, omit the `input` property in your action definition.

The following example shows a validated newsletter registration form that accepts a user’s email and requires a “terms of service” agreement checkbox.

1. 
Create an HTML form component with unique `name` attributes on each input:
2. 
Define a `newsletter` action to handle the submitted form. Validate the`email` field using the`z.email()` validator, and the`terms` checkbox using`z.boolean()` :See the[`input` API reference](/en/reference/modules/astro-actions/#input-validator) for all available form validators.
3. 
Add a `<script>` to the HTML form to submit the user input. This example overrides the form’s default submit behavior to call`actions.newsletter()` , and redirects to`/confirmation` using the`navigate()` function:See[“Call actions from an HTML form action”](#call-actions-from-an-html-form-action) for an alternative way to submit form data.

### Displaying form input errors

[Section titled “Displaying form input errors”](#displaying-form-input-errors)

You can validate form inputs before submission using [native HTML form validation attributes](https://developer.mozilla.org/en-US/docs/Learn/Forms/Form_validation#using_built-in_form_validation) like `required`, `type="email"`, and `pattern`. For more complex `input` validation on the backend, you can use the provided [`isInputError()`](/en/reference/modules/astro-actions/#isinputerror) utility function.

To retrieve input errors, use the `isInputError()` utility to check whether an error was caused by invalid input. Input errors contain a `fields` object with messages for each input name that failed to validate. You can use these messages to prompt your user to correct their submission.

The following example checks the error with `isInputError()`, then checks whether the error is in the email field, before finally creating a message from the errors. You can use JavaScript DOM manipulation or your preferred UI framework to display this message to users.

## Call actions from an HTML form action

[Section titled “Call actions from an HTML form action”](#call-actions-from-an-html-form-action)

Pages must be on-demand rendered when calling actions using a form action. [Ensure prerendering is disabled on the page](/en/guides/on-demand-rendering/#enabling-on-demand-rendering) before using this API.

You can enable zero-JS form submissions with standard attributes on any `<form>` element.  Form submissions without client-side JavaScript may be useful both as a fallback for when JavaScript fails to load, or if you prefer to handle forms entirely from the server.

Calling [Astro.getActionResult()](/en/reference/api-reference/#getactionresult) on the server returns the result of your form submission (`data` or `error`), and can be used to dynamically redirect, handle form errors, update the UI, and more.

To call an action from an HTML form, add `method="POST"` to your `<form>`, then set the form’s `action` attribute using your action, for example `action={actions.logout}`. This will set the `action` attribute to use a query string that is handled by the server automatically.

For example, this Astro component calls the `logout` action when the button is clicked and reloads the current page:

Additional attributes on the `<form>` element may be necessary for proper schema validation with Zod. For example, to include file uploads, add `enctype="multipart/form-data"` to ensure that files are sent in a format correctly recognized by `z.instanceof(File)`:

### Redirect on action success

[Section titled “Redirect on action success”](#redirect-on-action-success)

If you need to redirect to a new route on success, you can use an action’s result on the server. A common example is creating a product record and redirecting to the new product’s page, e.g. `/products/[id]`.

For example, say you have a `createProduct` action that returns the generated product id:

You can retrieve the action result from your Astro component by calling `Astro.getActionResult()`. This returns an object containing `data` or `error` properties when an action is called, or `undefined` if the action was not called during this request.

Use the `data` property to construct a URL to use with `Astro.redirect()`:

### Handle form action errors

[Section titled “Handle form action errors”](#handle-form-action-errors)

Calling `Astro.getActionResult()` in the Astro component containing your form gives you access to the `data` and `error` objects for custom error handling.

The following example displays a general failure message when a `newsletter` action fails:

For more customization, you can [use the `isInputError()` utility](#displaying-form-input-errors) to check whether an error is caused by invalid input.

The following example renders an error banner under the `email` input field when an invalid email is submitted:

#### Preserve input values on error

[Section titled “Preserve input values on error”](#preserve-input-values-on-error)

Inputs will be cleared whenever a form is submitted. To persist input values, you can [enable view transitions](/en/guides/view-transitions/#enabling-view-transitions-spa-mode) and apply the `transition:persist` directive to each input:

### Update the UI with a form action result

[Section titled “Update the UI with a form action result”](#update-the-ui-with-a-form-action-result)

To use an action’s return value to display a notification to the user on success, pass the action to `Astro.getActionResult()`. Use the returned `data` property to render the UI you want to display.

This example uses the `productName` property returned by an `addToCart` action to show a success message.

### Advanced: Persist action results with a session

[Section titled “Advanced: Persist action results with a session”](#advanced-persist-action-results-with-a-session)

	**Added in:**
	`astro@5.0.0`
	
	

Action results are displayed as a POST submission. This means that the result will be reset to `undefined` when a user closes and revisits the page. The user will also see a “confirm form resubmission?” dialog if they attempt to refresh the page.

To customize this behavior, you can add middleware to handle the result of the action manually. You may choose to persist the action result using a cookie or session storage.

Start by [creating a middleware file](/en/guides/middleware/) and importing [the `getActionContext()` utility](/en/reference/modules/astro-actions/#getactioncontext) from `astro:actions`. This function returns an `action` object with information about the incoming action request, including the action handler and whether the action was called from an HTML form. `getActionContext()` also returns the `setActionResult()` and `serializeActionResult()` functions to programmatically set the value returned by `Astro.getActionResult()`:

A common practice to persist HTML form results is the [POST / Redirect / GET pattern](https://en.wikipedia.org/wiki/Post/Redirect/Get). This redirect removes the “confirm form resubmission?” dialog when the page is refreshed, and allows action results to be persisted throughout the user’s session.

This example applies the POST / Redirect / GET pattern to all form submissions using session storage with the [Netlify server adapter](/en/guides/integrations-guide/netlify/) installed. Action results are written to a session store using [Netlify Blob](https://docs.netlify.com/blobs/overview/), and retrieved after a redirect using a session ID:

## Security when using actions

[Section titled “Security when using actions”](#security-when-using-actions)

Actions are accessible as public endpoints based on the name of the action. For example, the action `blog.like()` will be accessible from `/_actions/blog.like`. This is useful for unit testing action results and debugging production errors. However, this means you **must** use the same authorization checks that you would consider for API endpoints and on-demand rendered pages.

### Authorize users from an action handler

[Section titled “Authorize users from an action handler”](#authorize-users-from-an-action-handler)

To authorize action requests, add an authentication check to your action handler. You may want to use [an authentication library](/en/guides/authentication/) to handle session management and user information.

Actions expose [a subset of the `APIContext` object](/en/reference/modules/astro-actions/#actionapicontext) to access properties passed from middleware using `context.locals`. When a user is not authorized, you can raise an `ActionError` with the `UNAUTHORIZED` code:

### Gate actions from middleware

[Section titled “Gate actions from middleware”](#gate-actions-from-middleware)

	**Added in:**
	`astro@5.0.0`
	
	

Astro recommends authorizing user sessions from your action handler to respect permission levels and rate-limiting on a per-action basis. However, you can also gate requests to all actions (or a subset of actions) from middleware.

Use the [`getActionContext()` function](/en/reference/modules/astro-actions/#getactioncontext) from your middleware to retrieve information about any inbound action requests. This includes the action name and whether that action was called using a client-side remote procedure call (RPC) function (e.g. `actions.blog.like()`) or an HTML form.

The following example rejects all action requests that do not have a valid session token. If the check fails, a “Forbidden” response is returned. Note: this method ensures that actions are only accessible when a session is present, but is *not* a substitute for secure authorization.

## Call actions from Astro components and server endpoints

[Section titled “Call actions from Astro components and server endpoints”](#call-actions-from-astro-components-and-server-endpoints)

You can call actions directly from Astro component scripts using the `Astro.callAction()` wrapper (or `context.callAction()` when using a [server endpoint](/en/guides/endpoints/#server-endpoints-api-routes)). This is common to reuse logic from your actions in other server code.

Pass the action as the first argument and any input parameters as the second argument. This returns the same `data` and `error` objects you receive when calling actions on the client:

[Contribute](/en/contribute/)

[Community](https://astro.build/chat)

[Sponsor](https://opencollective.com/astrodotbuild)

# Citations

1. Source page: https://docs.astro.build/en/guides/actions
