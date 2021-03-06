---
title: Fractal API documentation
handle: api
---

Fractal provides a programmatic API that allows you to {{ link('@custom-commands', 'write custom commands') }}, {{ link('@build-tools', 'tie it into your build tools') }} or help with integrating your component library into your {{ link('@production', 'production site or application') }}.

If you've created a {{ link('@project-settings', 'project settings file') }} for your project then you have already interacted with the Fractal API.

<div class="Note Note--callout">
<p>The Fractal API docs are currently very much a <strong>work in progress</strong>. Keep checking back regularly for updates!</p>
</div>

## Obtaining a Fractal instance

All API methods are called on an instance of Fractal or one of the objects it exposes. To get a new instance of Fractal, first `require` the `@frctl/fractal` module and then call the `.create()` method on it. In one line that looks like this:

```js
const fractal = require('@frctl/fractal').create();
```

You can then call API methods on this fractal instance (or on the objects it exposes) like so:

```js
// set the project title
fractal.set('project.title', 'My New Project');
```

See the individual API documentation pages for full details of available properties and methods.

## Initial load & parse

Before you can access data about any components or documentation pages via the API, you need to first call the `fractal.load()` method to tell Fractal to perform an initial parse of the relevant filesystem directories. This method is asynchronous and returns a `Promise`:

```js
fractal.load().then(() => {

    // render a component with a custom set of context data
    fractal.components.render('@button', {
        text: 'Click here',
        style: 'primary-action'
    }).then(html => {
        console.log(html);
    });

});
```

This method is called behind the scenes when creating new development server instances or running CLI commands.
