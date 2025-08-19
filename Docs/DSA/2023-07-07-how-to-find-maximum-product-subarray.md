---
title: "How to find Maximum Product Subarray?"
date: 2023-07-07 04:27:19
categories: ['Array-Strings']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/maximum-product-subarray/description/" target="_blank" rel="noopener" title="">: </a>Given an integer array <code>nums</code>, find a subarray that has the largest product, and return <em>the product</em>. The test cases are generated so that the answer will fit in a <strong>32-bit</strong> integer.


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<strong>Example 1:</strong>


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Input:</strong> nums = 
<strong>Output:</strong> 6
<strong>Explanation:</strong>  has the largest product 6.
</pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<strong>Example 2:</strong>


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Input:</strong> nums = 
<strong>Output:</strong> 0
<strong>Explanation:</strong> The result cannot be 2, because  is not a subarray.
</pre>
<!-- /wp:preformatted -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: O(N)
// SC: O(1)
func maxProductSubArray(_ arr: ) ->Int {
    var prod1 = arr
    var prod2 = arr
    var result = arr
    
    for i in 1..<arr.count {
        var temp = max(arr,max(prod1*arr, prod2*arr))
        prod2 = min(arr, min(prod1*arr, prod2*arr))
        prod1 = temp
        result = max(result, prod1)
    }
    
    return result
}
var inputMaxProductSubArray = 
var outputMaxProductSubArray = maxProductSubArray(nums)
print("The maximum product subarray is: ", outputMaxProductSubArray)// 4</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->



<!-- /wp:paragraph -->