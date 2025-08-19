---
title: "How to use  typealias in swift ?"
date: 2022-10-13 09:44:30
categories: ['iOS', 'Swift', 'typealias closure swift', 'typealias in swift example']
layout: post
---

<!-- wp:paragraph -->
<strong>typealias</strong> also known as <strong>type-Identifier</strong>. so basically we are defining a substitute of a type. For example we can give type of <strong>String</strong> to <strong>Str</strong> as - <code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">typealias Str = String </mark></code>so now onwards you can use <em>Str</em> instead of <em>String</em>


<!-- /wp:paragraph -->

<!-- wp:heading {"level":4} -->
<h4><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">1. Basic Example with data type</mark></h4>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">typealias Str = String
let x: Str = "Boom"
print(x) // prints Boom</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
You might thinking what's the big thing in it? But it is. Let suppose you have a complex statement like closure etc so you can shrink it down with substitute so your code will look much cleaner, let me explain you with example :


<!-- /wp:paragraph -->

<!-- wp:heading {"level":4} -->
<h4><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">2. typealias with closure: </mark></h4>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">typealias customBlock =  (()->Void)

func signIn(userID:String, completion: @escaping customBlock) {
    completion()
}

signIn(userID: "11") { dataObject in
    print(dataObject)
}</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
So here we have used <code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">customBlock</mark></code> which act as as <code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">typealias</mark></code> which declare as a closure. So you might required same block in your project which can be replace shorter. In this way this can easily readable & reduce code density. like wise you can try with <code>Result<DataObj, Error> </code>for your network call modules.


<!-- /wp:paragraph -->

<!-- wp:heading {"level":4} -->
<h4><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">3. Multiple Protocols with typealias: </mark></h4>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">typealias multipleProtocol = NSObjectProtocol & NSCopying & NSCoding
var xValue: multipleProtocol</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
Here we have used multiple protocols with <code>typealias</code>, so you can just use <code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">multipleProtocol</mark></code> which act as a<code> NSObjectProtocol & NSCopying & NSCoding</code>.. much cleaner huh!! 😤😤


<!-- /wp:paragraph -->