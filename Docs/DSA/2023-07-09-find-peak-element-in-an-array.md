---
title: "Find Peak Element in an Array"
date: 2023-07-09 14:24:27
categories: ['BinarySearch']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/find-peak-element/description/" target="_blank" rel="noopener" title="">: </a>Given a <strong>0-indexed</strong> integer array <code>nums</code>, find a peak element, and return its index. If the array contains multiple peaks, return the index to <strong>any of the peaks</strong>.


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<strong>Example 1:</strong>


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Input:</strong> nums = 
<strong>Output:</strong> 2
<strong>Explanation:</strong> 3 is a peak element and your function should return the index number 2.</pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<strong>Example 2:</strong>


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Input:</strong> nums = 
<strong>Output:</strong> 5
<strong>Explanation:</strong> Your function can return either index number 1 where the peak element is 2, or index number 5 where the peak element is 6.</pre>
<!-- /wp:preformatted -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: O(log(N))
// SC: O(1)
func findPeakElement(_ nums: ) -> Int {
    if nums.isEmpty  { return 0 }
    
    var left = 0
    var right = nums.count - 1
    
    while left < right {// from 0 to end of the array
        let mid = (left + right) / 2
        if nums < nums { // 3 < 5
            left = mid + 1
        } else {
            right = mid
        }
    }
    
    return left
}</code></pre>
<!-- /wp:code -->