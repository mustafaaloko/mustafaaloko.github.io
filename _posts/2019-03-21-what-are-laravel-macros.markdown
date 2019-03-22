---
title:  "What are Laravel Macros?"
description: "How to leverage the power of Laravel Macros to write expressive code."
date: 21-Mar-2019
---

## What good Laravel Macros bring?

Have you ever been in a situation that you wanted a method or functionality to be part of Laravel's core, but for one or another reason it isn't? I get this feeling a lot, especially when writing tests and working with collections. It's not possible to have everything one needs in a tool or a framework like Laravel. There will always be the need for our own utilities and abstractions to better solve some project-specific problems.

Macros are there to help us exactly with these situations. With Macros we can extend the power of Laravel's components/classes in a very easy, clean and expressive way. 

In the below example, we will add a method named <span>`evens()`</span> to the Laravel's Collection class, this method will return only even numbers in an array.

{% highlight php %}
use Illuminate\Support\Collection;

Collection::macro('evens', function() {
    return $this->filter(function($value) {
        return $value % 2 === 0;
    });
});

// Now the above can be used as below:
$collection = collect([3, 5, 8, 2, 1, 6]);

$collection->evens(); 

// [8, 2, 6]
{% endhighlight %}

Notice how <span>`$this`</span> inside <span>`Collection::macro`</span> is bound to the instance of <span>`Illuminate\Support\Collection`</span> class. This will help more with our code's expresiveness by providing more context inside <span>`macro()`</span>, we will be able to use lots of existing methods on that class. Remember, <span>`$this`</span> always binds to the instance of the class we are creating Macro for. 

## Where to define them?

As Macros are added in the runtime, therefore the best place to define them are inside [Laravel's Service Providers](https://laravel.com/docs/5.8/providers). This will make sure that our newly added methods will be available nearly everywhere in our code. We can add them in the<span> `AppServiceProvider`</span> as shown in the below example or inside a more specific service provider that we may wanna create for this purpose.

{% highlight php %}
<?php

namespace App\Providers;

use Illuminate\Support\ServiceProvider;
use Illuminate\Support\Collection;

class AppServiceProvider extends ServiceProvider
{
    /**
     * Register any application services.
     *
     * @return void
     */
    public function register()
    {
        Collection::macro('evens', function() {
            return $this->filter(function($value) {
                return $value % 2 === 0;
            });
        });
    }
}
{% endhighlight %}

## How to know if a component is macro-able?

There are around 20 classes in Laravel which are macro-able. If a class is using <span>`Illuminate\Support\Traits\Macroable`</span> trait, it's "Macroable". See the <span>`Illuminate\Support\Arr`</span> class as an example:

<div>
    <a href="/assets/images/laravel-macros/arr-class.png" class="image">
        <img src="/assets/images/laravel-macros/arr-class.png" alt="">
    </a>
</div>

## Some Practical Examples

In one of my projects, I added some utility assertion methods (Macros) for <span>`Illuminate\Foundation\Testing\TestResponse`</span> class to have some expressive and clean assertions.

Using these assertions I can do:

{% highlight php %}
/** @test */
public function it_creates_a_user()
{
    $response = $this->json('POST', '/api/user', ['name' => 'Ahmad']);

    $response->assertCreated();
}
{% endhighlight %}

Instead of:

{% highlight php %}
/** @test */
public function it_creates_a_user()
{
    $response = $this->json('POST', '/api/user', ['name' => 'Ahmad']);

    $response->assertStatus(Response::HTTP_CREATED);
}
{% endhighlight %}

Of course, I used above example to describe the concept easily. Macros can be used to simplify much more complicated logic. You can find a more advanced example in below. There are 4 macro examples, you can go through each one of them to understand what they actually do.

<div>
    <a href="/assets/images/laravel-macros/test-response-examples.png" class="image">
        <img src="/assets/images/laravel-macros/test-response-examples.png" alt="">
    </a>
</div>

That's it. Thank you for reading this. Let me know if you have any questions or comments in below.