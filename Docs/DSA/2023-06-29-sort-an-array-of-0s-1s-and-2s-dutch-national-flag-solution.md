---
title: "Sort an array of 0s, 1s and 2s || Dutch National Flag solution"
date: 2023-06-29 12:06:30
categories: ['Array-Strings']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/sort-colors/description/" target="_blank" rel="noopener" title="">:</a> How to sort an array which has 0s, 1s and 2s


<!-- /wp:paragraph -->

<!-- wp:heading {"level":6} -->
<h6 class="wp-block-heading">Approach #1 Using Dutch National Flag </h6>
<!-- /wp:heading -->

<!-- wp:paragraph -->
I used three pointers low mid & high The sorting of 0,1,2 is as per below steps <br>arr contains 0.  <br>arr contains 1<br>arr contains 2. ,<br>So we swap according to the left(0) mid(1) & hight(2) position


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func sortZerosOnesTwos(nums: inout ) {
    var low = 0
    var high = nums.count - 1
    var mid = 0
    
    while mid <= high {
        let item = nums
        switch item {
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
var miscArray = 
sortZerosOnesTwos(nums: &miscArray)
print("After sorting 0's, 1's, 2's", miscArray) //</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->



<!-- /wp:paragraph -->