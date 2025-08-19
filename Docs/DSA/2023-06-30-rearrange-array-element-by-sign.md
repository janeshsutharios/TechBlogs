---
title: "Rearrange array element by sign"
date: 2023-06-30 03:58:08
categories: ['Array-Strings']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/rearrange-array-elements-by-sign/description/" target="_blank" rel="noopener" title="">:</a> An given array contains equal number of positive and negative elements. Without altering the relative order of positive and negative elements, you must return an array of alternately positive and negative values.<br>Example: --<br>Input:  {1,2,-4,-5}<br>Output: 1 -4 2 -5


<!-- /wp:paragraph -->

<!-- wp:heading {"level":6} -->
<h6 class="wp-block-heading">Approach #1 </h6>
<!-- /wp:heading -->

<!-- wp:paragraph -->
As positive index is on even numbers so create variable named positiveIndex with 0 & negativeIndex with 1 and increment the index by +2 after fill.


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: O(n)
// SC: O(1)
func arrangeArray(arr: ) ->  {
    var positiveIndex = 0
    var negativeIndex = 1
    var arrangedArray = Array.init(repeating: 0, count: arr.count)
    for i in 0..<arr.count {
        if arr < 0 {
            arrangedArray = arr;
            negativeIndex += 2;
        } else {
            arrangedArray = arr;
            positiveIndex += 2;
        }
    }
    return arrangedArray
}

var mixArray = 
let opArrangedArr = arrangeArray(arr: mixArray)
print("The op Arranged Arr  is:", opArrangedArr)// </code></pre>
<!-- /wp:code -->