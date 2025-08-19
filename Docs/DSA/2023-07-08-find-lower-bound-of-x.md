---
title: "Find Lower bound of x"
date: 2023-07-08 11:23:15
categories: ['BinarySearch']
layout: post
---

<!-- wp:paragraph -->
:  Given a sorted array <strong> </strong>and an integer x, write a program to find the lower bound of x.(arr >= x))


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Example 1:</strong>
<strong>Input Format:</strong> N = 4, arr = {1,2,2,3}, x = 2
<strong>Result:</strong> 1
<strong>Explanation:</strong> Index 1 is the smallest index such that arr >= x.

<strong>Example 2:</strong>
<strong>Input Format:</strong> N = 5, arr = {3,5,8,15,19}, x = 9
<strong>Result:</strong> 3
<strong>Explanation:</strong> Index 3 is the smallest index such that arr >= x.</pre>
<!-- /wp:preformatted -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: O(log(N))
// SC: O(1)
func findLowerBound(_ arr: , _ targetElement: Int) -> Int {
    let arrayCount = arr.count
    var low = 0
    var high = arrayCount - 1
    var ans = arrayCount

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

var arrInputLowerBound = 
let targetElementLowerBound = 9
let indexLowerBoundOutput = findLowerBound(arrInputLowerBound, targetElementLowerBound)
print("The lower bound is the index:", indexLowerBoundOutput)// 3 hence  & (arr >= x))</code></pre>
<!-- /wp:code -->