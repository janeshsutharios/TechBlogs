---
title: "How to sort 0s 1s & 2s for an array in swift?"
date: 2022-12-24 15:50:56
categories: ['Array sort in swift', 'Array-Strings']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/sort-colors/description/" target="_blank" rel="noopener" title="">: </a>In a given array sort all 0s 1s & 2s .For example: I/P <em>{0, 1, 2, 0, 1, 2}</em>   o/p:: {<em>0, 0, 1, 1, 2, 2}</em><br>Solution:- We can use three pointers low, mid & high. Where low & mid is start index(i.e. 0) & high is arrayLength - 1. In a while loop we traverse mid to high & exit from loop when    <mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color"><strong>while</strong> mid <= high {</mark><br><strong>Special Note: </strong>We swap from Low (0) & High(2) As simple as that. So we don't move 1s & it by default will be in middle.


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func sortColors(_ nums: inout ) {
    var low = 0
    var high = nums.count - 1
    var mid = 0
    
    while mid <= high {
        switch nums {
        case 0:
            nums.swapAt(low,mid)
            low += 1
            mid += 1
        case 2:
            nums.swapAt(mid,high)
            high -= 1
        case 1:
            mid += 1
        default:
            continue
        }
    }
}
var nums = 
sortColors(&nums)
print("sort--->", nums)// prints.  </code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->



<!-- /wp:paragraph -->