---
title: "Find Kth Missing Positive Number"
date: 2023-07-11 11:21:20
categories: ['BinarySearch']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/kth-missing-positive-number/description/" target="_blank" rel="noopener" title="">: </a>Given an array <code>arr</code> of positive integers sorted in a <strong>strictly increasing order</strong>, and an integer <code>k</code>. Return <em>the</em> <code>k<sup>th</sup></code> <em><strong>positive</strong> integer that is <strong>missing</strong> from this array.</em>


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<strong>Example 1:</strong>


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Input:</strong> arr = , k = 5
<strong>Output:</strong> 9
<strong>Explanation: </strong>The missing positive integers are . The 5<sup>th</sup> missing positive integer is 9.</pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<strong>Example 2:</strong>


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Input:</strong> arr = , k = 2
<strong>Output:</strong> 6
<strong>Explanation: </strong>The missing positive integers are . The 2<sup>nd</sup> missing positive integer is 6.</pre>
<!-- /wp:preformatted -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: O(Nlog(N))
// SC: O(1)
func findKthPositive(_ arr: , _ k: Int) -> Int {
    var left = 0
    var right = arr.count - 1
    while left <= right {
        let mid = left + (right-left)/2
        if arr - mid - 1 < k {
            left = mid + 1
        } else {
            right = mid - 1
        }
    }
    return left + k
}
</code></pre>
<!-- /wp:code -->