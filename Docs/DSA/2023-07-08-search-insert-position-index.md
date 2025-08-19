---
title: "Search Insert position index"
date: 2023-07-08 12:04:40
categories: ['BinarySearch']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/search-insert-position/" target="_blank" rel="noopener" title="">: </a> Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order. You must write an algorithm with <code>O(log n)</code> runtime complexity.


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">Example 1:
Input: nums = , target = 5
Output: 2
Example 2:

Input: nums = , target = 2
Output: 1

Example 3:
Input: nums = , target = 7
Output: 4</pre>
<!-- /wp:preformatted -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: O(log(N))
// SC: O(1)
func findInsertPosition(_ arr: , _ targetElement: Int) -> Int {
    let arrayCount = arr.count
    var low = 0
    var high = arrayCount - 1
    var ans = arrayCount// So if element is greater it would be the last

    while low <= high {
        let mid = (low + high) / 2
        // maybe an answer
        if arr >= targetElement {
            ans = mid
            // look for smaller index on the left
            high = mid - 1
        } else {
            low = mid + 1 // look on the right
        }
    }
    return ans
}

var arrInputInsertPosition = 
let elementToInsert = 2
let positionOfLower = findInsertPosition(arrInputInsertPosition, elementToInsert)
print("The positionOfLower index will be ", positionOfLower) // index 1 Because </code></pre>
<!-- /wp:code -->