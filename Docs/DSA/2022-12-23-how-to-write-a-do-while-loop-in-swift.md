---
title: "How to write a do while loop in swift ?"
date: 2022-12-23 12:10:26
categories: ['How to create loop in swift', 'iOS', 'Swift']
layout: post
---

<!-- wp:paragraph -->
We can use <mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">repeat-while</mark> which is equivalent to <mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">do-while</mark> loop in swift. Here the single passthrough will happens first after that condition will be verified 


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">var n = 5
repeat {
    n -= 1
    print("value of n-->", n)// prints 4 to -1
} while n >= 0;</code></pre>
<!-- /wp:code -->