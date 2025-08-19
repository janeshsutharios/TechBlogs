---
title: "Subarray Sum Equals K"
date: 2023-07-19 17:22:27
categories: ['Array-Strings']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/subarray-sum-equals-k/description/" target="_blank" rel="noopener" title="">: </a>In an array <code>nums</code> and an integer <code>k</code>, return <em>the total number of subarrays whose sum equals to</em> <code>k</code>.


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<strong>Example 1:</strong>


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Input:</strong> nums = , k = 2
<strong>Output:</strong> 2</pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<strong>Example 2:</strong>


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Input:</strong> nums = , k = 3
<strong>Output:</strong> 2</pre>
<!-- /wp:preformatted -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: O(n)
// SC: O(n)
func subarraySumK(_ arr: , _ k: Int) ->Int {
    var result = 0, sum = 0
    var dict:  = 
    dict = 1
    for num in arr {
        sum += num
        if let val = dict {
            result += val
        }
        dict += 1// Storing the previous sum value which can be added to result.
    }
    return result
}

let subArr = 
let kSum = 3
let opKsum = subarraySumK(subArr, kSum)
print(" subArr with k sum is-->", opKsum)// 2 (1,2 & 3)</code></pre>
<!-- /wp:code -->

<!-- wp:image {"id":2048,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large">![](/TechBlogs/Assets/Website/2023/07/SubArray-sum-equalsK-1024x684.jpg)</figure>
<!-- /wp:image -->