---
title: "Find the Smallest Divisor Given a Threshold"
date: 2023-07-11 10:06:15
categories: ['BinarySearch']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/find-the-smallest-divisor-given-a-threshold/" target="_blank" rel="noopener" title=""></a>  Given an array of integers <code>nums</code> and an integer <code>threshold</code>, we will choose a positive integer <code>divisor</code>, divide all the array by it, and sum the division's result. Find the <strong>smallest</strong> <code>divisor</code> such that the result mentioned above is less than or equal to <code>threshold</code>.


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
Each result of the division is rounded to the nearest integer greater than or equal to that element. (For example: <code>7/3 = 3</code> and <code>10/2 = 5</code>).


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<strong>Example 1:</strong>


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Input:</strong> nums = , threshold = 6
<strong>Output:</strong> 5
<strong>Explanation:</strong> We can get a sum to 17 (1+2+5+9) if the divisor is 1. 
If the divisor is 4 we can get a sum of 7 (1+1+2+3) and if the divisor is 5 the sum will be 5 (1+1+1+2).</pre>
<!-- /wp:preformatted -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: O(N⋅log⁡M)
// SC: O(1)

// Return the sum of division results with 'divisor'.
func findDivisionSum(_ nums: , _ divisor: Int) -> Int {
    var result: Int = 0
    for num in nums {
        result += Int(ceil(Double(num) / Double(divisor))) // Get Higher/ Ceil Value
    }
    return result
}

func smallestDivisor(_ nums: , _ threshold: Int) -> Int {
    var low: Int = 1
    var high: Int = 0
    for num in nums {
        high = max(high, num)
    }
    
    // Iterate using binary search on all divisors.
    while low <= high {
        let mid: Int = (low + high) / 2
        let result: Int = findDivisionSum(nums, mid)
        // If current divisor does not exceed threshold,
        // then it can be our answer, but also try smaller divisors
        // thus change search space to left half.
        if result <= threshold {
            high = mid - 1
        }
        // Otherwise, we need a bigger divisor to reduce the result sum
        // thus change search space to right half.
        else {
            low = mid + 1
        }
    }
    return low
}

let ipArraySmallDivision = 
let divisiorThreshold = 6
let opDivisior = smallestDivisor(ipArraySmallDivision, divisiorThreshold)
print("opDivisior--- ", opDivisior) // 5</code></pre>
<!-- /wp:code -->