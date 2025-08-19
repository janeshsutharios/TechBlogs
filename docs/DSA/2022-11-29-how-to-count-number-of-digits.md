---
title: "How to count number of digits ?"
date: 2022-11-29 10:08:30
categories: ['Array-Strings', 'DSA', 'how to compute the number of digits of a number']
layout: post
---

<!-- wp:paragraph -->
The good approach will be to use <mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">log10</mark> Time complexity O(1) Space complexity O(1) . The number of digits in an integer = the upper bound of log10(n).<br>Example: log10(12345.0)) = > <strong>4.091491094267951</strong> so we have to use 4+1


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">print ("count the number of digits = ", Int(log10(12345.0))+1)// prints 5</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
Read more about Logarithm here<a href="https://janeshswift.com/ios/dsa/math/logarithms-explained/" target="_blank" rel="noopener" title=""> https://janeshswift.com/ios/dsa/math/logarithms-explained/</a>


<!-- /wp:paragraph -->