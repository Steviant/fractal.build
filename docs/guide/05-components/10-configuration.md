---
handle: components-config
label: Config reference
title: Configuring Components
---

Components and component {{ link('@collections', 'collections') }} can have their own (optional) configuration files associated with them. {{ link('@variants', 'Component variants') }} are configured within their parent component's configuration file.

If you haven't already, you should read the {{ link('@configuration-files', 'configuration file documentation') }} to learn more about how configuration files need to be named and formatted.

## Component properties

### collated

If set to true, individual variants of this component will not be visible in the web UI - instead the preview of this component will concatenate all variants together into a single preview.

```yaml
collated: false
```
### context

The {{ link('@context-data', 'context data') }} to pass to the template when rendering previews.

`context` is an **inheritable property**. Any context data set on the component will be *merged* with context data set upstream in the {{ link('@configuration-files#configuration-inheritance', 'configuration cascade') }}.

```yaml
context:
  buttonText: 'Click here!'
  listItems: ['foo','bar','baz']
```

### display

CSS property key/value pairs that preview UIs *may* choose to use to apply to the preview rendering area. Useful for doing things like setting max-widths for components that are designed to only be used in sidebars.

This *does not* leak into the styling of the component itself; it is just applied to the area (typically an iframe) that the component is previewed within in plugins such as the web preview UI.

```yaml
display:
  max-width: 400px
  min-width: 250px
```

### handle

Override the generated handle. Note that this will also have the side effect of preventing any [prefixes](#prefix) set in upstream collections being applied to the handle.

```yaml
handle: my-great-component
```

### hidden

Specifies whether the component is hidden (i.e. does not show up in listings or navigation) or not. Overrides the inferred value from an underscore-prefixed file name if set.

```yaml
hidden: true
```

### label

The label is typically displayed in any UI navigation items that refer to the component. Defaults to a title-cased version of the component name if not specified.

```yaml
label: 'Mega Buttons'
```

### name

Overrides the component name, which is otherwise extracted from the component view filename. Name values must be all lowercase, and contain only alphanumeric characters with hyphens or underscores for word seperators.

Setting this will also have the affect of changing the {{ link('@naming', 'component\'s handle') }}.

```yaml
name: 'mega-buttons'
```

### notes

Any notes about the component. Displayed in the web preview UI if present. Any notes set here override content taken from the component's README.md file, if there is one.  Accepts markdown.

```yaml
notes: Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

### order

An integer order value, used when sorting components. Overrides any order value set as a property of the filename if set.

```yaml
order: 4
```

### preview

Which layout (specified by {{ link('@naming', 'handle') }}) to use to when rendering previews of this layout. See the {{ link('@preview-layouts', 'preview layouts') }} documentation for more details

```yaml
preview: '@my-preview-layout'
```
### status

The status of a component. See the {{ link('@statuses', 'statuses documentation') }} for information on using and customising component statuses.

`status` is an **inheritable property**. If not set directly on the component it will inherit any status set further up in the {{ link('@configuration-files#configuration-inheritance', 'configuration cascade') }}.

```yaml
status: 'wip'
```
* **Choices:** `prototype | wip | ready`

### title

The title of a component is typically what is displayed at the top of any pages related to the component. Defaults to the same as the `label` if not specified.

```yaml
title: 'Amazing Mega Buttons'
```

### tags

An array of tags to add to the component. Can be used by plugins and tasks to filter components.

`tags` is an **inheritable property**. Tags set on the component will be *merged* with tags set upstream in the {{ link('@configuration-files#configuration-inheritance', 'configuration cascade') }}.

```yaml
tags: ['sprint-1', 'foobar']
```

### variants

An array of variant configuration objects. See the variant properties options (below) and the {{ link('@variants', 'variants documentation') }} for more information on working with variants.

Many variant properties are **inherited from the parent component**, and all apart from the `name` value are optional.

```yaml
variants:
  - name: 'large'
    status: 'ready'
    context:
      buttonText: "I'm a large button!"
  - name: 'small'
    context:
      isSmall: true
```
## Variant properties

Variants can be defined in the parent components configuration file. See the {{ link('@variants', 'variants documentation') }} for full details on creating and configuring variants.

### context

The {{ link('@context-data', 'context data') }} to pass to the variant view template when rendering previews.

Any context set on a variant will be merged with it's parent component's (inherited and merged) context data.

```yaml
context:
  buttonText: 'It's a unicorn button!'
```

### display

Set the component display property description for details. This is merged with any display properties assigned to the parent content.

```yaml
display:
  max-width: 300px
```

### name

The name of the variant. This is the only **mandatory property** for variant definitions.

A variant with a name of 'large' that belongs to the component named 'button' will have a {{ link('@naming', 'handle') }} of **@button--large**.

```yaml
name: 'unicorn'
```

### notes

Any notes about the variant. Displayed in the web preview UI if present. Accepts markdown.

```yaml
notes: "Different from the default component because this one is *funky*."
```

### preview

Which layout (specified by it's {{ link('@naming', 'handle') }} to use to when rendering previews of this layout. See the {{ link('@preview-layouts', 'preview layouts') }} documentation for more details.

This overrides any the (inherited) `preview` value of the parent component.

```yaml
preview: '@my-special-layout'
```

### status

The status of the variant. Overrides the default status of it's parent component.

```yaml
status: 'wip'
```
* **Choices:** `prototype | wip | ready`

### view

The view file to use. If not specified and a view file matching the variant's handle is found (i.e. `component--variant.hbs` or similar) then that view will be used. If none is specified and no matching template is found, then the view file for the parent component will be used.

```yaml
view: 'component--funky.hbs'
```

## Collection properties

Collections can specify properties that should be applied to all child components of that collection via {{ link('@configuration-files#configuration-inheritance', 'configuration cascade') }}. See the {{ link('@collections', 'documentation on collections') }} for more details on how to work with collections, and for details on available non-inheritable properties like `label` and `title`.

### collated

Whether or not child components of this collection [should be collated](#collated) or not.

```yaml
collated: false
```

### context

{{ link('@context-data', 'context data') }} to be applied to children of the collection. Any context set on a collection will be merged into any contexts set by it's children.

```yaml
context:
  buttonText: 'It's a unicorn button!'
```

### display

Display property options for child components. This is merged with any display properties set on individual child components.

```yaml
display:
  max-width: 300px
```

### preview

The default preview layout (specified by it's {{ link('@naming', 'handle') }} that child components should when being rendered as a preview. See the {{ link('@preview-layouts', 'preview layouts') }} documentation for more details.

```yaml
preview: '@my-special-layout'
```

### prefix

A string to be prefixed on to the generated {{ link('@naming', 'handles') }} of all components (and variants) in that collection.

```yaml
prefix: 'atoms'
```
Given the prefix above, a component with the name of `button` that lives within this collection will have the handle `@atoms-button`.

### status

The default status for all children of the collection.

```yaml
status: 'wip'
```
* **Choices:** `prototype | wip | ready`

### tags

An array of tags to add to all child components. Will be merged together with any tags specified on the components themselves.

```yaml
tags: ['sprint-1', 'foobar']
```

## Example component configuration file

A fairly full-featured, JS-formatted example component config file may look something like this:

```js
module.exports = {
	title: "Amazing Mega Buttons",
	status: "prototype",
	tags: ['sprint-1', 'author:mark'],
	preview: '@preview-layout',
	context: {
		"button-text": "Click me!",
		"is-sparkly": true
	},
	variants: [{
		name: 'large',
		notes: 'Only use this when you need a really big button!',
		context: {
			modifier: 'is-large'
		}
	},{
		name: 'warning',
		status: 'wip',
		context: {
			modifier: 'is-warning',
			button-text: 'Do not click'
		}
	}]
};
```