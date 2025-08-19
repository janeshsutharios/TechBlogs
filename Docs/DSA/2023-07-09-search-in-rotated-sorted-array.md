---
title: "Search in Rotated Sorted Array"
date: 2023-07-09 04:48:45
categories: ['BinarySearch']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/search-in-rotated-sorted-array/description/" target="_blank" rel="noopener" title=""> </a>In a given arra<code>y</code> which is sorted in ascending order (with <strong>distinct</strong> values). return <em>the index of </em><code>target</code><em> if it is in </em><code>nums</code><em>, or </em><code>-1</code><em> if it is not in </em><code>nums</code>.


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<strong>Example 1:</strong>


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Input:</strong> nums = , target = 0
<strong>Output:</strong> 4</pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<strong>Example 2:</strong>


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Input:</strong> nums = , target = 3
<strong>Output:</strong> -1</pre>
<!-- /wp:preformatted -->

<!-- wp:heading {"level":6} -->
<h6 class="wp-block-heading">#Approach: Using Binary search</h6>
<!-- /wp:heading -->

<!-- wp:paragraph -->
We can find element using binary search,  we will see first in left half of array than right half of the array and if target element found as mid element return it which is the answer.


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// Question 8: Search element in rotated sorted array
// TC: O(log(N))
// SC: O(1)
func searchInRotated(nums: , targetElement: Int) ->Int {
    var low = 0
    var high = nums.count - 1
    while low <= high {
        let mid = (low + high) / 2
        
        // if mid points to the target
        if nums == targetElement {
            return mid
        }
        
        // if left part is sorted
        if nums <= nums {
            if nums <= targetElement && targetElement <= nums {
                // element exists
                high = mid - 1
            } else {
                // element does not exist
                low = mid + 1
            }
        } else { // if right part is sorted
            if nums <= targetElement && targetElement <= nums {
                // element exists
                low = mid + 1
            } else {
                // element does not exist
                high = mid - 1
            }
        }
    }
    return -1
}

let rotatedSortedArr = 
let targetElInRotated = 1
let opFoundIndex = searchInRotated(nums: rotatedSortedArr, targetElement: targetElInRotated)
print(" Index found is-->", opFoundIndex) // 3</code></pre>
<!-- /wp:code -->