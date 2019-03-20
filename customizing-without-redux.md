---
layout: post
title: Customizing without Redux
---

# What if you don't want to use Redux
The `pwa-starter-kit` is supposed to be the well-lit path to building a fairly complex PWA, but it should in no way feel restrictive. If you know what you're doing, and don't want to use Redux to manage your application's state, that's totally fine! We've created a separate template, [`template-no-redux`](https://github.com/Polymer/pwa-starter-kit/tree/template-no-redux), that has the same UI and PWA elements as the main template, but does not have Redux.

Instead, it uses a unidirectional data flow approach: some elements are in charge of [maintaining the state](https://github.com/Polymer/pwa-starter-kit/blob/template-no-redux/src/components/my-view2.js#L44) for their section of the application:

```js
static get properties() {
  return {
    _clicks: { type: Number },
    _value: { type: Number },
  }
}
```

They [pass that data down](https://github.com/Polymer/pwa-starter-kit/blob/template-no-redux/src/components/my-view2.js#L35) to children elements:

```html
<counter-element
  value="${this._value}"
  clicks="${this._clicks}">
</counter-element>
```

{:.fyi}
Note the `${this.PROPERTY}` syntax is [LitElement's method of data binding](https://lit-element.polymer-project.org/docs/templates/databinding), which is the same syntax for passing an expression to a [JavaScript template literal](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals).

In response, when the children elements need to update the state, they [fire an event](https://github.com/Polymer/pwa-starter-kit/blob/template-no-redux/src/components/counter-element.js#L56):

```js
_onIncrement() {
  this.dispatchEvent(new CustomEvent('counter-incremented'));
}
```

And those [events can easily be listened for](https://github.com/Polymer/pwa-starter-kit/blob/template-no-redux/src/components/my-view2.js#L36-L37) with [LitElement's declarative data binding event handler syntax](https://lit-element.polymer-project.org/docs/templates/syntax):
```html
<counter-element
    @counter-incremented="${this._increment}"
    @counter-decremented="${this._decrement}">
</counter-element>
```

{:.fyi}
In the above example, `@counter-incremented` listens for a `counter-incremented` event and calls `this._increment` when it receives it. `@counter-decremented` listens for a `counter-decremented` and then calls `this._decrement`.

# Exercises

{:.instructions}
Here are two updates to make to our counter in my-view2.js. Before attempting these updates, there are 2 important prerequisites:

1. Make sure you are working in your `pwa-starter-kit-no-redux` project
2. There is a bug in the `my-view2.js` file in `template-no-redux` where

```html
<div class="circle">${this._clicks}</div>
```

should be

```html
<div class="circle">${this._value}</div>
```

[Make that change](https://github.com/ComcastSamples/pwa-starter-kit-no-redux/commit/dddc43a892bbe611d94839a58f1abe9a67cc27d5) and then give these 2 exercises a try:

{:.instructions}
1) Add a "Reset" button that resets the "clicked" and "value" counters to `0`.

{:.instructions}
2) Add a "Double Increment" toggle that causes the "+" and "-" buttons to increment/decrement by 2 when it is toggled on.

## Next step
For a small app like this, you can see [you might not need Redux](https://medium.com/@dan_abramov/you-might-not-need-redux-be46360cf367). But as you build a more complex app, Redux can be very useful. So let's look at how we can build this same PWA with Redux in the next step:
- [Redux and State Management]({{site.baseurl}}/redux-and-state-management).
