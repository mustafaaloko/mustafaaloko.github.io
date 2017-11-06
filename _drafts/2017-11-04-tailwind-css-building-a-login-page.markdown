---
title:  "Tailwind CSS - Building a Login Page"
description: We will try to build a beautiful login page with Tailwind CSS without writing any line of CSS code 
date: 02-Nov-2017
---

Finally, after months of waiting, [Tailwind CSS][tailwind-website] is released. I am not a frontend pro, but I think that as a developer utility-first CSS frameworks like Tailwind can help me design custom and at the same time beautiful user interfaces. According to many, Tailwind will be a big deal in near future.

In this post we will create a beautiful login page using Tailwind. I will try to keep things as simple as possible. We won't touch using Tailwind with PostCSS, Webpack, Laravel Mix or others, instead we will only concentrate on Tailwind itself.

Below is our completed designed page, which we will build with Tailwind in this post.

<div>
    <a href="/assets/images/tailwind/complete.png" class="image">
        <img src="/assets/images/tailwind/complete.png" alt="">
    </a>
</div>

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

Final step will be to compile <span>`style.css`</span> with Tailwind's build engine to use it in our regular HTML. Below command will create a <span>`dist.css`</span>.

{% highlight shell %}
$ ./node_modules/.bin/tailwind build style.css -o dist.css
{% endhighlight %}

<hr>

## Writing the login HTML
Above is all what we need to get started with Tailwind. For bigger projects, we may need to use PostCSS with Tailwind, which I will try to cover in other posts.

Before we get into using Tailwind specific utilities, we will create our page's HTML structure. Below is a pure HTML structure of the page we want to build.

{% highlight html %}
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">

    <!-- This is our compiled CSS file which is created by Tailwind CLI -->
    <link rel="stylesheet" href="dist.css">

    <title>Login</title>
</head>
<body>
    <div>
        <div>
            <h1>Login to our Website</h1>
            <div>
                <div>
                    <label>Username or Email</label>
                    <input type="text" placeholder="Your Username">
                </div>
                <div>
                    <label>Password</label>
                    <input type="text" placeholder="Your Password">
                </div>
                <div>
                    <button>Login</button>
                    <a href="#">Forgot Password?</a>
                </div>
            </div>
            <div>
                <p>Don't have an account? <a href="#">Create an Account</a>.</p>
            </div>
        </div>
    </div>
</body>
</html>
{% endhighlight %}

If you notice in the above code, we don't have a single class attribute defined in any of HTML tags. We will go tag by tag and style them using our Tailwind CSS utilities. Below image is how our current HTML page will look.

<div>
    <a href="/assets/images/tailwind/html.png" class="image">
        <img src="/assets/images/tailwind/html.png" alt="">
    </a>
</div>

#### Basic Page Styling
Before we start anything, we have to setup our basic stuff like, background color, maximum page height and others. We can directly apply these classes to body element as below.

{% highlight html %}
...
<body class="bg-grey-lighter h-screen font-sans">
...
</body>
...
{% endhighlight %}

In above example, we have used three classes from Tailwind utilities. Each one is described in below.

- **Background color:** We used <span>`bg-grey-lighter`</span> to give light grey color to the background. The syntax for this is <span>`bg-{color}`</span>. Where color can be anything from values mentioned in [background docs](https://tailwindcss.com/docs/background-color) and [color docs](https://tailwindcss.com/docs/colors/).
- **Screen Height:** Class <span>`h-screen`</span> will make the element height same as screen height, it's 100vh in CSS. You can use the <span>`h-{size}`</span> class for this.
- **Font Family:** This class sets our body font family to sans family of fonts. 

> Please remember that in some cases you can refer to your Tailwind config file which in this case is <span>`tailwind.js`</span> and use it as a documentation. Comments are really well written and descriptive.

> You can easily configure Tailwind for your more custom use, you can go to Tailwind's config file <span>`tailwind.js`</span> and add or change values for different options the way you like. Please remember that you need to re-build your <span>`dist.css`</span> to have the changes affected after you make any change to <span>`tailwind.js`</span>.

#### Centering (Positioning) Elements

Tailwind provides utilities to use Flexbox easily. As per our final design, we have to vertically and horizontally center all of our page's elements. Let's see how we can do it using Flexbox and some other Tailwind utilities.

{% highlight html %}
...
<body class="bg-grey-lighter h-screen font-sans">
    <div class="container mx-auto h-full flex justify-center items-center">
        <div class="w-1/3">
            <h1 class="font-hairline mb-6 text-center">Login to our Website</h1>
            ...
            </h1>
        </div>
    </div>
</body>
...
{% endhighlight %}

- **Container:** This utility (<span>`container`</span>) works same as Bootstrap's container, setting up max-width of the page. The only difference is that Tailwind doesn't add margin's automatically to left and right of the element to center it on the page. Therefore, we need to add <span>`mx-auto`</span> to center the element.
- **Height 100%:** We use <span>`h-full`</span> to stretch the height of element same of its parent height. It is same as <span>`height: 100%`</span>. Refer to official docs of [height](https://tailwindcss.com/docs/height) and [width](https://tailwindcss.com/docs/width) for more details.
- ****


[tailwind-website]: https://tailwindcss.com
[tailwind-github]:  https://github.com/tailwindcss/tailwindcss
