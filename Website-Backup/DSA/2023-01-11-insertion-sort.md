---
title: "Insertion Sort"
date: 2023-01-11 10:05:49
categories: ['insertion sort in swift', 'Sorting', 'sorting in swift']
layout: post
---

<!-- wp:paragraph -->
# Approach Assume two part of the array sorted & unsorted. Sorted start from 1 element A & fills with unsorted one by one (A to A) Attached code with dry run.


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// Insertion Sort
// TC: O(n^2) worst . O(n). Best
// SC: O(1)
func insertionSort(_ arr: inout ) {
    
    for i in 1..<arr.count {
        var current = arr
        var j = i - 1
        while j >= 0 && arr > current {
            arr = arr
            j -= 1
        }
        arr = current
       // print("arr-->", arr, j)
    }
}


var arrayToSort:  = 
insertionSort(&arrayToSort)
print("Sorted Array--> ", arrayToSort) // </code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
 In Insertion sort we sort using two sets. One is Sorted set Another is unsorted one. Initially we sorted is index 0 element & rest is unsorted set. Now we move forward one by one with unsorted array & compare element & pick element from unsorted to sorted one At the right place.<While finding the right place we swap element using inner while loop>


<!-- /wp:paragraph -->

<!-- wp:image {"id":1735,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large">![](/TechBlogs/Assets/Website/2023/01/Insertion-sort-swift-2-791x1024.png)</figure>
<!-- /wp:image -->