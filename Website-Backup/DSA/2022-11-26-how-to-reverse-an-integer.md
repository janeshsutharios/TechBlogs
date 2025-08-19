---
title: "How to reverse an Integer ?"
date: 2022-11-26 13:51:41
categories: ['Array-Strings', 'DSA', 'reverse Integer in swift']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/reverse-integer/description/" target="_blank" rel="noopener" title="">: </a>Reverse Integer in swift ex. 12345 => 54321 output should lie in Int32 Range


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
TC: O(n)<br>SC: O(1)


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func reverse(_ x: Int) -> Int {
    var r = 0, x = x
    while x != 0 {
        r = r * 10
        r = r + (x % 10)
        x /= 10
    }
    return r < Int32.min || r > Int32.max ? 0 : r
}
print(reverse(12345))</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
Explanation: Here we are multiplying result with10 further adding it to modulo(reminder) & get last element by divide by 10


<!-- /wp:paragraph -->

<!-- wp:paragraph {"style":{"elements":{"link":{"color":{"text":"var:preset|color|ast-global-color-1"}}}},"textColor":"ast-global-color-1"} -->
<p class="has-ast-global-color-1-color has-text-color has-link-color"><strong>Example - 7913 ==== <em>3197</em></strong>


<!-- /wp:paragraph -->

<!-- wp:table -->
<figure class="wp-block-table"><table><tbody><tr><td>r</td><td>0</td><td>30</td><td>310</td><td>3190</td></tr><tr><td>r</td><td>3</td><td>31</td><td>319</td><td>3197</td></tr><tr><td>x</td><td>791</td><td>79</td><td>7</td><td>0</td></tr></tbody></table><figcaption class="wp-element-caption">This is explanation of code</figcaption></figure>
<!-- /wp:table -->