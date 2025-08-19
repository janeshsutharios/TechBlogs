---
title: "Split Array Largest Sum"
date: 2023-07-12 10:19:04
categories: ['BinarySearch']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/split-array-largest-sum/description/" target="_blank" rel="noopener" title="">:</a> Given an integer array <code>nums</code> and an integer <code>k</code>, split <code>nums</code> into <code>k</code> non-empty subarrays such that the largest sum of any subarray is <strong>minimized</strong>. Return <em>the minimized largest sum of the split</em>.


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
A <strong>subarray</strong> is a contiguous part of the array.


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<strong>Example 1:</strong>


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Input:</strong> nums = , k = 2
<strong>Output:</strong> 18
<strong>Explanation:</strong> There are four ways to split nums into two subarrays.
The best way is to split it into  and , where the largest sum among the two subarrays is only 18.</pre>
<!-- /wp:preformatted -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: O(Nlog(N))
// SC: O(1)
func splitArray(_ nums: , _ splitValue: Int) -> Int {
    //-1. find the boundary
    var left = 0, right = 0
    for num in nums {
        left = max(num, left)
        right += num
    }
    
    var result = Int.max
    while left <= right {
        let mid = left + (right - left)/2
        if isValidSplitSum(nums, mid, splitValue) {
            result = min(result, mid)
            right = mid - 1
        } else {
            left = mid + 1
        }
    }
    return result
}

private func isValidSplitSum(_ nums: , _ aSplitSum: Int, _ splitValue: Int) -> Bool {
    var count = 1
    var current = 0
    for i in 0..<nums.count {
        current += nums
        if nums > aSplitSum {
            return false
        }
        if current > aSplitSum {
            current = nums
            count += 1
        }
    }
    return count <= splitValue
}
let arrSplitArray = 
let splitInto = 2
let opSplitSum = splitArray(arrSplitArray, splitInto)
print("op Split Sum ", opSplitSum)// 18 which is 10+8  </code></pre>
<!-- /wp:code -->