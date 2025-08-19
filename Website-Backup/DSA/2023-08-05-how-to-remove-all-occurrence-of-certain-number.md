---
title: "How to Remove all occurrence of certain number ?"
date: 2023-08-05 16:33:32
categories: ['Array-Strings']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/remove-element/description/" target="_blank" rel="noopener" title="">: </a>Given an integer array <code>nums</code> and an integer <code>k</code>, remove all occurrences of <code>k</code> in <code>nums</code> <a href="https://en.wikipedia.org/wiki/In-place_algorithm" target="_blank" rel="noreferrer noopener"><strong>in-place</strong></a>. The order of the elements may be changed. Then return <em>the </em>count after removal


<!-- /wp:paragraph -->

<!-- wp:heading {"level":5} -->
<h5 class="wp-block-heading">Approach:</h5>
<!-- /wp:heading -->

<!-- wp:paragraph -->
We can declare a variable which holds index initial it's 0 now move elements which are not matched with k 


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: O(n)
// SC: O(1)
func removeElement(_ nums: inout , _ val: Int) -> Int {
    var count = 0
    for i in 0..<nums.count where nums != val {
        nums = nums
        count+=1
    }
    return count
}
var arrOcc = 
removeElement(&arrOcc, 2)
//print("Output after removal --", arrOcc)//</code></pre>
<!-- /wp:code -->