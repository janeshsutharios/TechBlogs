---
title: "Draw Recursion Stack"
date: 2023-01-21 11:00:16
categories: ['Recursion', 'Recursion examples in swift', 'recursion in swift']
layout: post
---

<!-- wp:paragraph -->
: Prepare recursion stack for multilevel recursion. 


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func test(_ curr: Int) {
    //print("fuction-->", curr)
    if curr < 2 {
        print("first", curr)
        test(curr+1)
        print("second", curr)
        test(curr+1)
        print("Final---------> ", curr)
    }
}
test(0)
// This Prints --->
first 0
first 1
second 1
Final--------->  1
second 0
first 1
second 1
Final--------->  1
Final--------->  0</code></pre>
<!-- /wp:code -->

<!-- wp:image {"id":1746,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large">![](/TechBlogs/Assets/Website/2023/01/recursion-stack-1024x765.jpg)</figure>
<!-- /wp:image -->

<!-- wp:paragraph -->



<!-- /wp:paragraph -->