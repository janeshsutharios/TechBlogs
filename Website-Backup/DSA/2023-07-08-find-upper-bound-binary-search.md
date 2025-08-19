---
title: "Find Upper bound: Binary Search"
date: 2023-07-08 11:38:24
categories: ['BinarySearch']
layout: post
---

<!-- wp:paragraph -->
<a href="https://takeuforward.org/arrays/implement-upper-bound/" target="_blank" rel="noopener" title="">: </a>Upper Bound || Given a sorted array of N integers and an integer x, write a program to find the upper bound of x.


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Example 1:</strong>
<strong>Input Format:</strong> N = 4, arr = {1,2,2,3}, x = 2
<strong>Result:</strong> 3
<strong>Explanation:</strong> Index 3 is the smallest index such that arr > x.

<strong>Example 2:</strong>
<strong>Input Format:</strong> N = 6, arr = {3,5,8,9,15,19}, x = 9
<strong>Result:</strong> 4
<strong>Explanation:</strong> Index 4 is the smallest index such that arr > x.</pre>
<!-- /wp:preformatted -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: O(log(N))
// SC: O(1)
func findUpperBound(_ arr: , _ targetElement: Int) -> Int {
    let arrayCount = arr.count
    var low = 0
    var high = arrayCount - 1
    var ans = arrayCount

    while low <= high {
        let mid = (low + high) / 2
        // maybe an answer
        if arr > targetElement {
            ans = mid
            // look for smaller index on the left
            high = mid - 1
        } else {
            low = mid + 1 // look on the right
        }
    }
    return ans
}
var arrInputUpperBound = 
let targetElementUpperBound = 9
let indexUpperBoundOutput = findUpperBound(arrInputUpperBound, targetElementUpperBound)
print("The Upper bound is the index:", indexUpperBoundOutput)// 4 hence </code></pre>
<!-- /wp:code -->