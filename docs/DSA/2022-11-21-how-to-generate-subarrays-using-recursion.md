---
title: "How to Generate subarrays using recursion"
date: 2022-11-21 10:45:21
categories: ['DSA', 'generating subarrays', 'Recursion']
layout: post
---

<!-- wp:paragraph -->
: We haveGiven an array, generate all the possible subarrays of the given array using recursion for example : 


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">  n = 3   Array =    Output =        </code></pre>
<!-- /wp:code -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func printAllSequence(currentIndex: Int, op: inout , inArray: ,length: Int) {
    if currentIndex == length {
        print(op)
        return
    }
    op.append(inArray)
    printAllSequence(currentIndex: currentIndex+1, op: &op, inArray: inArray, length: length)
    op.removeLast()
    printAllSequence(currentIndex: currentIndex+1, op: &op, inArray: inArray, length: length)
}


var inArray = 
var length = inArray.count
var op:  = 
var currentIndex = 0
printAllSequence(currentIndex: currentIndex, op: &op, inArray: inArray, length: length)</code></pre>
<!-- /wp:code -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">It prints -->        </code></pre>
<!-- /wp:code -->

<!-- wp:image {"id":1549,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large">![](/TechBlogs/Assets/Website/2022/11/print_all_sequence-1-1024x780.jpg)</figure>
<!-- /wp:image -->