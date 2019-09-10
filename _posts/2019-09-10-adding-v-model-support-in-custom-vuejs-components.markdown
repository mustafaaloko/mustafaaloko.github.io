---
title:  "Adding v-model Support to Custom Vue.js Components"
description: "Let's see how we can add two-way data-binding support in our custom Vue.js components"
date: 10-Sep-2019
---

## Overview

Almost everyone who has worked with Vue.js for few hours knows how two-way data-binding works in form elements. Below snippet shows a very basic example of this data-binding. We have used <span>`v-model`</span> directive to bind <span>`message`</span> from app state to the <span>`input`</span> form element. If you change the input, the DOM (anywhere <span>`message`</span> is used) will update itself without any explicit code written.

<p class="codepen" data-height="265" data-theme-id="0" data-default-tab="html,result" data-user="mustafaaloko" data-slug-hash="pozLPjo" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="pozLPjo">
  <span>See the Pen <a href="https://codepen.io/mustafaaloko/pen/pozLPjo/">
  pozLPjo</a> by Mustafa Ehsan (<a href="https://codepen.io/mustafaaloko">@mustafaaloko</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

<br>

## How it works under the hood?

Any component or element which supports <span>`v-model`</span> out of the box adheres to this contract: accept a prop named <span>`value`</span> and emit an <span>`input`</span> event to trigger a data change. Basically, <span>`<input v-model="message" />`</span> is a shorthand for writing <span>`<input :value="message" @input="message = $event.target.value />"`</span>. Below code achieves the same result as in the first example without using <span>`v-model`</span>.

<p class="codepen" data-height="265" data-theme-id="0" data-default-tab="html,result" data-user="mustafaaloko" data-slug-hash="QWLmvMw" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Vue.js Data-Binding Example without v-model">
  <span>See the Pen <a href="https://codepen.io/mustafaaloko/pen/QWLmvMw/">
  Vue.js Data-Binding Example without v-model</a> by Mustafa Ehsan (<a href="https://codepen.io/mustafaaloko">@mustafaaloko</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>
<br>

## How to add <span>`v-model`</span> support in custom components?

Now let's see how we can add this support in our custom components neatly and without extra or useless code. The idea is that how we can allow our child components to modify its parent component's state.

In our custom component, all we need to do is accept a <span>`value`</span> prop and emit an <span>`input`</span> event on a value change that we want to notify child component's parent about. Any value which will be passed as the emitted event argument will be passed to parent component to maintain its state.

In the below example, we are creating a custom component named <span>`text-input`</span> which is a re-usable custom input component we may wanna use for our project. To make sure that it operates same as HTML's native <span>`input`</span> element, we will add <span>`v-model`</span> support as below:

<p class="codepen" data-height="265" data-theme-id="0" data-default-tab="js,result" data-user="mustafaaloko" data-slug-hash="RwbMxOx" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Custom Vue.js Component with v-model Support">
  <span>See the Pen <a href="https://codepen.io/mustafaaloko/pen/RwbMxOx/">
  Custom Vue.js Component with v-model Support</a> by Mustafa Ehsan (<a href="https://codepen.io/mustafaaloko">@mustafaaloko</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>
<br>

As shown in the above example, we are calling <span>`onInputChange`</span> on the <span>`input`</span> element's value change which in turn emits the event that we discussed above. That's it, now you can see that our custom element (<span>`<text-input v-model="message" />`</span>) supports the <span>`v-model`</span> directive same as our plain input elements.