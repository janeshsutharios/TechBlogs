---
title: "Search Single Element in a sorted array"
date: 2023-07-09 16:18:21
categories: ['BinarySearch']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/single-element-in-a-sorted-array/description/" target="_blank" rel="noopener" title="">: </a>You are given a sorted array consisting of only integers where every element appears exactly twice, except for one element which appears exactly once.<br>Return <em>the single element that appears only once</em>.<br>Your solution must run in <code>O(log n)</code> time and <code>O(1)</code> space.


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<strong>Example 1:</strong>


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Input:</strong> nums = 
<strong>Output:</strong> 2</pre>
<!-- /wp:preformatted -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// Approach #1 using reduce
func singleNonDuplicate(_ nums: ) -> Int {
    nums.reduce(0, ^)
}
// Approach #2
// TC: O(logN)
// SC: O(1)
func singleNonDup(_ nums: ) ->Int {
    if nums.isEmpty { return -1 }
    var left = 0
    var right = nums.count - 1
    
    while left < right {
        var mid = (left + right)/2
        if (mid % 2 == 0 && nums == nums) || (mid % 2 == 1 && nums == nums) {
            // If mid is even & so dup will be next number
            // If mid is Odd & so dup will be prev number
            left = mid + 1
        } else {
            right = mid
        }
    }
    return nums
}
let dupArray = 
let singleEl = singleNonDuplicate(dupArray)
print("singleEl is --- ", singleEl) //singleEl 10

let uniqueEl = singleNonDup(dupArray)
print("singleEl is --- ", uniqueEl) //singleEl 10
</code></pre>
<!-- /wp:code -->