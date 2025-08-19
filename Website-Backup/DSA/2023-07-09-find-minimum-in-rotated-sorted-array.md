---
title: "Find Minimum in Rotated Sorted Array"
date: 2023-07-09 06:08:27
categories: ['BinarySearch']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/description/" target="_blank" rel="noopener" title="">: </a>Suppose an array of length <code>n</code> sorted in ascending order is <strong>rotated</strong> between <code>1</code> and <code>n</code> times. For example, the array <code>nums = </code> might become:


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<code></code> if it was rotated <code>4</code> times.


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<code></code> if it was rotated <code>7</code> times.


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
Notice that <strong>rotating</strong> an array <code>, a, a, ..., a]</code> 1 time results in the array <code>, a, a, a, ..., a]</code>.<br>Given the sorted rotated array <code>nums</code> of <strong>unique</strong> elements, return <em>the minimum element of this array</em>.<br>You must write an algorithm that runs in <code>O(log n) time.</code>


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<strong>Example 1:</strong>


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Input:</strong> nums = 
<strong>Output:</strong> 1
<strong>Explanation:</strong> The original array was  rotated 3 times.</pre>
<!-- /wp:preformatted -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: O(log(N))
// SC: O(1)
func findMin(_ nums: ) ->Int {
    
    var low = 0
    var high = nums.count - 1
    var ans = Int.max
    while low <= high {
        let mid = (low + high) / 2
        //search space is already sorted
        //then arr will always be
        //the minimum in that search space:
        if nums <= nums {
            ans = min(ans, nums)
            break
        }
        
        // If left part is sorted:
        if nums <= nums {
            // Keep the minimum:
            ans = min(ans, nums)

            // Eliminate left half:
            low = mid + 1
        } else { // If right part is sorted:
            // Keep the minimum:
            ans = min(ans, nums)

            // Eliminate right half:
            high = mid - 1
        }
    }
    return ans
}

let rotArrayInput = 
let rotArrayOutput = findMin(rotArrayInput)
print("The minimum element is: ", rotArrayOutput)// 0</code></pre>
<!-- /wp:code -->