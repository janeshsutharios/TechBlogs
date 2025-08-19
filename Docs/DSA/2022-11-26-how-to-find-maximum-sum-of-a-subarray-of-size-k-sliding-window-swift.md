---
title: "How to find maximum  sum of a subarray of size k - Sliding window swift"
date: 2022-11-26 06:40:11
categories: ['Array-Strings', 'DSA', 'sliding window swift']
layout: post
---

<!-- wp:paragraph -->
<a href="https://www.geeksforgeeks.org/find-maximum-minimum-sum-subarray-size-k/" target="_blank" rel="noopener" title="">: </a> Find maximum  sum of a subarray of size k example , k: 4 = output: 21 (6+1+5+9)<br>Solution: with sliding window we can achieve. first we take sum of first k elements further move elements by 1 window size & add the latest var & remove last var.


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func findMaxSubArray(arr: , k: Int) ->Int {
    let size = arr.count
    if k > size { return -1 }
    var maxSum = 0
    for i in 0..<k {
        maxSum += arr
    }
    var thisSum = maxSum
    for i in k..<size {
        thisSum += arr - arr
// Add the difrence value from last to first
        maxSum = max(maxSum, thisSum)
    }
    return maxSum
    
}
print(findMaxSubArray(arr: , k: 4))</code></pre>
<!-- /wp:code -->