---
title:  "Tailwind CSS - Building a Login Page"
description: We will try to build a beautiful login page with Tailwind CSS without writing any line of CSS code 
date: 07-Nov-2017
---

Finally, after months of waiting, [Tailwind CSS][tailwind-website] has just been released. Through this post, I intend to build a beautiful login page using Tailwind. I will try to keep things as simple as possible. We will not cover things like using Tailwind with Webpack, Laravel Mix or others, instead we will only concentrate on Tailwind itself.

I am not a frontend pro, but I think that as a developer, a utility-first CSS framework like Tailwind can help me design custom and at the same time beautiful user interfaces. According to many, Tailwind will be a big deal in near future.

Below is our completed designed page, which we will build with Tailwind in this post.

<div>
    <a href="/assets/images/tailwind/complete.png" class="image">
        <img src="/assets/images/tailwind/complete.png" alt="">
    </a>
</div>

<hr>

## What is Tailwind CSS?
Tailwind is a utility-first CSS framework, think of it as a bunch of pre-written small and tiny CSS utilities/classes for your use. 

Unlike frameworks such as Bootstrap, Foundation and Bulma, there are no out of the box UI components. Instead, you can use Tailwind's utilities to build your own custom UI components, which offers a great deal of flexibility in your designing process. You won't be bound and dependent to your framework's design choices.

All of the above can be achieved even without writing a single line of CSS. To understand more on what Tailwind is and what it isn't, please refer to the official docs: [What is Tailwind?](https://tailwindcss.com/docs/what-is-tailwind).

<hr>

## Getting Started

#### Installation
We will start with an empty directory and we will use <span>`npm`</span> to install Tailwind. 

Create an empty directory named **tailwind-learning** and inside it run <span>`npm init`</span> to initialize the project. After that run the following command to fetch and install Tailwind from NPM repository.

{% highlight shell %}
$ npm install tailwindcss --save-dev
{% endhighlight %}


#### Basic Configuration
Tailwind needs at least two files to work with, a configuration file and a CSS file where you import Tailwind's base utilities.

Configuration file is the main place where all Tailwind related configs like options for colors, font sizes, borders and others exist. To create it, run the command:

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

Final step would be to compile <span>`style.css`</span> with Tailwind's build engine. This will generate a <span>`dist.css`</span> that we can include in our HTML page.

{% highlight shell %}
$ ./node_modules/.bin/tailwind build style.css -o dist.css
{% endhighlight %}

<hr>

## Writing the Login Page Markup
Above is all what we needed to get started with Tailwind. For bigger projects, we may need to use Webpack or other tools with Tailwind, which I aim to cover in upcoming posts.

Before we get into using Tailwind specific utilities, we will create our page's HTML structure. Below is a pure HTML structure of the page we want to build.

File: **login.html**
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

File: **login.html**
{% highlight html %}
...
<body class="bg-grey-lighter h-screen font-sans">
...
</body>
...
{% endhighlight %}

In above example, we have used three classes from Tailwind utilities. Each one is described in below.

- **Background color:** We used <span>`bg-grey-lighter`</span> to give light grey color to the background. The syntax for this is <span>`bg-{color}`</span>. Where color can be anything from values mentioned in [background docs](https://tailwindcss.com/docs/background-color) and [color docs](https://tailwindcss.com/docs/colors/).
- **Screen Height:** Class <span>`h-screen`</span> will make the element height same as screen height, it's 100vh in CSS. You can use the <span>`h-{size}`</span> syntax to use other values as well.
- **Font Family:** This class sets our body font family to sans family of fonts. 

> Keep in mind that in some cases you can refer to your Tailwind config file which in this case is <span>`tailwind.js`</span> and use it as a documentation. Comments are really well written and descriptive.

> You can easily configure Tailwind for your custom use, by going to Tailwind's config file <span>`tailwind.js`</span> and adding or changing values for different options the way you like. Please remember that you need to re-build your <span>`dist.css`</span> to have the changes affected after you make any change to <span>`tailwind.js`</span>.

#### Centering (Positioning) Elements

Tailwind provides utilities to use Flexbox easily. As per our final design, we have to vertically and horizontally center all of our page's elements. Let's see how we can do it using Flexbox and some other Tailwind utilities.

File: **login.html**
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
- **Height 100%:** We use <span>`h-full`</span> to stretch the height of an element same as that of its parent height, it is equivalent to <span>`height: 100%`</span>. Refer to official docs of [height](https://tailwindcss.com/docs/height) and [width](https://tailwindcss.com/docs/width) for more details.
- **Flexbox:** I must admit that Tailwind makes it enjoyable to use Flexbox. In our case, we have used <span>`flex`</span> to specify that we will be using CSS flex display and we have added <span>`justify-center`</span> and <span>`items-center`</span> to horizontally and vertically center the child elements inside our div.
- **Elements Widths:** We can use <span>`w-{size}`</span> syntax to specify the width of our elements. In this case we are using <span>`w-1/3`</span> to set the width of our element to one third of its parent element. It's equivalent to set an element class to <span>`col-md-4 col-md-offset-4`</span> in Bootstrap.
- **Text Styling and Positioning:** There are several ways to style text in Tailwind. In above, <span>`font-hairline`</span> sets the CSS <span>`font-weight`</span> property to <span>`100`</span> and <span>`text-center`</span> is equivalent to CSS's <span>`text-align: center`</span>.
- **Margins and Paddings:**: This is one of my favorite parts. You no longer need to shift between your HTML and CSS files to set different margin and padding sizes for your elements. In Tailwind, you can easily use <span>`p{side?}-{size}`</span> and <span>`m{side?}-{size}`</span> to add margins and paddings. We have used <span>`mb-6`</span> which sets the bottom margin of our header to **1.5rem**. Below is a list of possible values we can replace with **size** placeholder in above example.

File: **tailwind.js**
{% highlight javascript %}
...
  margin: {
    'px': '1px',
    '0': '0',
    '1': '0.25rem',
    '2': '0.5rem',
    '3': '0.75rem',
    '4': '1rem',
    '6': '1.5rem',
    '8': '2rem',
  },
...
{% endhighlight %}

Please note that as mentioned before, you can change or add values to all options which exist in <span>`tailwind.js`</span> file.

Following is the screenshot of how our page looks like with all the code we have written so far.

<div>
    <a href="/assets/images/tailwind/step2.png" class="image">
        <img src="/assets/images/tailwind/step2.png" alt="">
    </a>
</div>

Positioning looks good, now we need to concentrate on our labels, form fields and buttons styling.

#### Form Elements Styling and CSS Pseudo-classes
In this section, we will not be covering each and every field and part of the form, but we will only cover new utilities. For the remaining elements, you have to figure it out on your own using the existing knowledge you have gained through this post.

File: **login.html**
{% highlight html %}
...
<div class="border-teal p-8 border-t-12 bg-white mb-6 rounded-lg shadow-lg">
    <div class="mb-4">
        <label class="font-bold text-grey-darker block mb-2">Username or Email</label>
        <input type="text" class="block appearance-none w-full bg-white border border-grey-light hover:border-grey px-2 py-2 rounded shadow" placeholder="Your Username">
    </div>
    ...
</div>
...
{% endhighlight %}

- **Login Box:** We have given our login box a white background (<span>`bg-white`</span>) along with shadows (<span>`shadow-lg`</span>) so it can stand out on our grey colored background page. We have also added a **1.5rem** bottom margin and a padding of **2rem** to all four sides.
- **Borders and Radius:** You can use <span>`border{-side?}{-width?}`</span> and <span>`border-{color}`</span> for specifying a border's width, color and side. <span>`rounded{-radius?}`</span> is used to set our border's radius.
- **Labels:** We put a small margin to the bottom of label using <span>`mb-2`</span> and also we have used <span>`font-bold`</span> to set our font's weight to bold. Both label and input use <span>`block`</span> utility which is same as <span>`display: block`</span> in CSS.
- **Appearance None:** If you want to remove and reset all browser default styling on an element, use <span>`appearance-none`</span> utility. This way you can fully customize the design of the elements you work with.
- **Hover:** If you want to add a specific style to an element on states like hover or focus, you can use <span>`hover:{whatever-style-class}`</span> syntax. In the above example, we change the text box border to darker grey when you hover on it (<span>`hover:border-grey`</span>). 

**Note:** We don't have a border width with value **12px** in Tailwind's config file by default. We have used this to give our login div's top border a size of **12px** (<span>`border-t-12`</span>). Please add it manually as shown below and then run the build command again to generate a new <span>`dist.css`</span>.

File: **tailwind.js**
{% highlight javascript %}
...
  borderWidths: {
    default: '1px',
    '0': '0',
    '2': '2px',
    '4': '4px',
    '8': '8px',
    '12': '12px' // Add it here
  },
...
{% endhighlight %}

<hr>

## Final Thoughts

I know that there are some confusions moving around your head right now, like Tailwind seems to be messing up my HTML code and there are lots of duplicate code written. Well, as I said in the beginning, this is a post that I tried to only cover the basics of Tailwind. You can easily abstract utilities by creating components and utilities in Tailwind. Please refer to [extracting components](https://tailwindcss.com/docs/extracting-components) and [adding new utilities](https://tailwindcss.com/docs/adding-new-utilities/) for more info.

I will cover Tailwind's advance-ish topics in upcoming posts.

Below is the full version of our code <span>`login.html`</span>. I have tried my best to cover the general parts of Tailwind in an easy way, please let me know through comments if I haven't done it in a good way.

File: **login.html**
{% highlight html %}
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">

    <link rel="stylesheet" href="dist.css">

    <title>Login</title>
</head>
<body class="bg-grey-lighter h-screen font-sans">
    <div class="container mx-auto h-full flex justify-center items-center">
        <div class="w-1/3">
            <h1 class="font-hairline mb-6 text-center">Login to our Website</h1>
            <div class="border-teal p-8 border-t-12 bg-white mb-6 rounded-lg shadow-lg">
                <div class="mb-4">
                    <label class="font-bold text-grey-darker block mb-2">Username or Email</label>
                    <input type="text" class="block appearance-none w-full bg-white border border-grey-light hover:border-grey px-2 py-2 rounded shadow" placeholder="Your Username">
                </div>

                <div class="mb-4">
                    <label class="font-bold text-grey-darker block mb-2">Password</label>
                    <input type="text" class="block appearance-none w-full bg-white border border-grey-light hover:border-grey px-2 py-2 rounded shadow" placeholder="Your Password">
                </div>

                <div class="flex items-center justify-between">
                    <button class="bg-teal-dark hover:bg-teal text-white font-bold py-2 px-4 rounded">
                        Login
                    </button>

                    <a class="no-underline inline-block align-baseline font-bold text-sm text-blue hover:text-blue-dark float-right" href="#">
                        Forgot Password?
                    </a>
                </div>
                
            </div>
            <div class="text-center">
                <p class="text-grey-dark text-sm">Don't have an account? <a href="#" class="no-underline text-blue font-bold">Create an Account</a>.</p>
            </div>
        </div>
    </div>
</body>
</html>
{% endhighlight %}

Below is how our final result will look like.

<div>
    <a href="/assets/images/tailwind/complete.png" class="image">
        <img src="/assets/images/tailwind/complete.png" alt="">
    </a>
</div>

That's it for now. I will cover more and more about Tailwind in my upcoming posts. Let me know of your suggestions through comments.

[tailwind-website]: https://tailwindcss.com
[tailwind-github]:  https://github.com/tailwindcss/tailwindcss
