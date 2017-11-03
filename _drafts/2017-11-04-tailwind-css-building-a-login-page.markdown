---
title:  "Tailwind CSS - Building a Login Page"
description: We will try to build a beautiful login page with Tailwind CSS without writing any line of CSS code 
date: 02-Nov-2017
---

Finally, after months of waiting [Tailwind CSS][tailwind-website] is released. I believe that it will be a big deal in near future.

In this post we will create a beautiful login page using Tailwind. I will try to keep things as simple possible. We won't touch using Tailwind with PostCSS, Webpack, Laravel Mix or others, instead we will only concentrate on Tailwind itself.

<hr>

## What is Tailwind CSS?
Tailwind is a utility-first CSS framework, think of it as a bunch of pre-written small and tiny CSS utilities/classes for your use. 

Unlike frameworks like Bootstrap, Foundation and Bulma, there are no out of the box UI components. Instead, you can use Tailwind's utilities to build your own custom UI components, which provides a huge flexibility in your designing process. You won't be bound and dependent to your framework's design choices.

All of the above can be achieved even without writing a single line of CSS. To understand more on what Tailwind is and what it isn't, please refer to the official docs: [What is Tailwind?](https://tailwindcss.com/docs/what-is-tailwind).

<hr>

## Getting Started

#### Installation
We will start with an empty directory and we will use <span>`npm`</span> to install Tailwind. 

Create an empty directory named **tailwind-learning** and inside it run <span>`npm init`</span> to initialize our project. After that run the below command to fetch and install Tailwind from NPM repository.

{% highlight shell %}
$ npm install tailwindcss --save-dev
{% endhighlight %}


#### Basic Configuration
Tailwind needs at least two files to work with, a configuration file and a CSS file where you import Tailwind's base utilities.

Configuration file is the main place where all Tailwind related configs like options for colors, font sizes, borders and others exist. To create it run the below command:

{% highlight shell %}
$ ./node_modules/.bin/tailwind init tailwind.js
{% endhighlight %}

Next, create a CSS file (style.css) where we will inject Tailwind's <span>`preflight`</span> and <span>`utilities`</span> styles using <span>`@tailwind`</span> directive. You can use this file to inject your own custom utilities and components, but to keep things simple, we will skip that for now.

File: **style.css**
{% highlight css %}
/**
 * This injects Tailwind's base styles, which is a combination of
 * Normalize.css and some additional base styles.
 *
 * You can see the styles here:
 * https://github.com/tailwindcss/tailwindcss/blob/master/css/preflight.css
 */
@tailwind preflight;

/**
 * Here you would add any of your custom component classes; stuff that you'd
 * want loaded *before* the utilities so that the utilities could still
 * override them.
 *
 * Example:
 * 
 * .btn { ... }
 * .form-input { ... }
 *
 * Or if using a preprocessor:
 * 
 * @import "components/buttons";
 * @import "components/forms";
 */

/**
 * This injects all of Tailwind's utility classes, generated based on your
 * config file.
 */
@tailwind utilities;

/**
 * Here you would add any custom utilities you need that don't come out of the
 * box with Tailwind.
 *
 * Example :
 *
 * .bg-pattern-graph-paper { ... }
 * .skew-45 { ... }
 *
 * Or if using a preprocessor..
 * 
 * @import "utilities/backgrond-patterns";
 * @import "utilities/skew-transforms";
 */
{% endhighlight %}

Final step will be to compile <span>`style.css`</span> with Tailwind's build engine to use it in our regular HTML. Below command will create a `dist.css`.

 {% highlight shell %}
$ ./node_modules/.bin/tailwind build style.css -o dist.css
{% endhighlight %}

<hr>

## Writing the login HTML
Above is all what we need to get started with Tailwind. For bigger projects, we may need to use PostCSS with Tailwind, which I will try to cover in other posts.

[tailwind-website]: https://tailwindcss.com
[tailwind-github]:  https://github.com/tailwindcss/tailwindcss
