---
title: "How to get the Power of Integer in Swift"
date: 2022-10-06 04:41:49
categories: ['iOS', 'pow swift example', 'Swift', 'swift cannot find pow in scope', 'swift math functions', 'swift pow integer', 'SwiftUI']
layout: post
---

<!-- wp:paragraph -->
In Swift we can use <code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">pow(<em>:</em>:)</mark></code> for making power of any number. For Example if we need 2 power 3  -


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">import Foundation 

let a = 2.0
let b = 3.0
let output = pow(a,b)// prints 8</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
Further you can also typeCaste to <code>Int</code> as    <code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color"> <strong>let</strong> output = Int(pow(a,b))</mark>// prints 8</code><br>Remember to add <code>import Foundation </code>for get rid of compile time error.


<!-- /wp:paragraph -->