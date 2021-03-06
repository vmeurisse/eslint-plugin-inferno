# Forbid certain elements (inferno/forbid-elements)

You may want to forbid usage of certain elements in favor of others, (e.g. forbid all `<div />` and use `<Box />` instead). This rule allows you to configure a list of forbidden elements and to specify their desired replacements.

## Rule Details

This rule checks all JSX elements and `Inferno.createElement` calls and verifies that no forbidden elements are used. This rule is off by default. If on, no elements are forbidden by default.

## Rule Options

```js
...
"inferno/forbid-elements": [<enabled>, { "forbid": [<string|object>] }]
...
```

### `forbid`

An array of strings and/or objects. An object in this array may have the following properties:

* `element` (required): the name of the forbidden element (e.g. `'button'`, `'Modal'`)
* `message`: additional message that gets reported

A string item in the array is a shorthand for `{ element: string }`.

The following patterns are not considered warnings:

```jsx
// [1, { "forbid": ["button"] }]
<Button />

// [1, { "forbid": [{ "element": "button" }] }]
<Button />
```

The following patterns are considered warnings:

```jsx
// [1, { "forbid": ["button"] }]
<button />
Inferno.createElement('button');

// [1, { "forbid": ["Modal"] }]
<Modal />
Inferno.createElement(Modal);

// [1, { "forbid": ["Namespaced.Element"] }]
<Namespaced.Element />
Inferno.createElement(Namespaced.Element);

// [1, { "forbid": [{ "element": "button", "message": "use <Button> instead" }, "input"] }]
<div><button /><input /></div>
Inferno.createElement('div', {}, Inferno.createElement('button', {}, Inferno.createElement('input')));
```

## When not to use

If you don't want to forbid any elements.
