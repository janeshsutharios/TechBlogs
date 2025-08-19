---
title: "Binary search: Find an element in an array"
date: 2023-07-08 10:32:41
categories: ['BinarySearch']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/binary-search/" target="_blank" rel="noopener" title=": ">: </a>Given an array of integers <code>nums</code> which is sorted in ascending order, and an integer <code>target</code>, write a function to search <code>target</code> in <code>nums</code>. If <code>target</code> exists, then return its index. Otherwise, return <code>-1</code>.<br>You must write an algorithm with <code>O(log n)</code> runtime complexity.


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<strong>Example 1:</strong>


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Input:</strong> nums = , target = 9
<strong>Output:</strong> 4
<strong>Explanation:</strong> 9 exists in nums and its index is 4</pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<strong>Example 2:</strong>


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Input:</strong> nums = , target = 2
<strong>Output:</strong> -1
<strong>Explanation:</strong> 2 does not exist in nums so return -1</pre>
<!-- /wp:preformatted -->

<!-- wp:heading {"level":5} -->
<h5 class="wp-block-heading">#Approach: Dividing array into two half and search target element</h5>
<!-- /wp:heading -->

<!-- wp:paragraph -->
We start dividing element into two half and & create a mid element until we match mid == target element<br>Here i have explained with two approach Iterative & recursive. 


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// Question: Binary search find array elements
// TC: O(logN), where N = size of the given array.
// SC O(1)If a number n can be divided by 2 for x times:
//2^x = n // Because we are dividing array by 2 every time.
//Therefore, x = logn (base is 2)
// Approach #1 Iterative approach.
func findElementUsingBinarySearch(nums: , target: Int) -> Int {
    let n = nums.count // size of the array
    var low = 0
    var high = n - 1
    // Divide the array until we got mid element as target element.
    while low <= high {
        let mid = (low + high) / 2
        if nums == target {
            return mid
        } else if target > nums {// If target is greater increase low pointer
            low = mid + 1
        } else {// If target is lesser decrease high pointer
            high = mid - 1
        }
    }
    return -1
}
// Approach #2 Recursion approach.
func findElementUsingBinarySearchUsingRecursion(nums: , target: Int, low: inout Int, high: inout Int) -> Int {
    if low > high { return -1 }// Base case.
    var mid = (low + high) / 2
    if nums == target {
        return mid
    } else if target > nums {// If target is greater increase low pointer
        low = mid + 1
    } else {// If target is lesser decrease high pointer
        high = mid - 1
    }
    // Divide the array until we got mid element as target element.
    return findElementUsingBinarySearchUsingRecursion(nums: nums, target: target, low: &low, high: &high)
}


let binaryArrayInput = 
let targetElementToFind = 6
let binaryIndexOutput = findElementUsingBinarySearch(nums: binaryArrayInput, target: targetElementToFind)
print("binaryIndexOutput ", binaryIndexOutput)// Output 2

// Using Recursion. ---
var high = binaryArrayInput.count - 1
var low = 0
let binaryIndexOutputRecursion = findElementUsingBinarySearchUsingRecursion(nums: binaryArrayInput, target: targetElementToFind, low: &low, high: &high)
print("findElementUsingBinarySearchUsingRecursion ", binaryIndexOutputRecursion) // Output 2</code></pre>
<!-- /wp:code -->