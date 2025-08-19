---
title: "Find Nth root using Binary search."
date: 2023-07-10 09:04:45
categories: ['BinarySearch']
layout: post
---

<!-- wp:paragraph -->
<a href="https://takeuforward.org/data-structure/nth-root-of-a-number-using-binary-search/" target="_blank" rel="noopener" title="">: </a>Given two numbers N and M, find the Nth root of M. The nth root of a number M is defined as a number X when raised to the power N equals M. If the ‘nth root is not an integer, return -1.


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Example 1:</strong>
<strong>Input Format:</strong> N = 3, M = 27
<strong>Result:</strong> 3
<strong>Explanation:</strong> The cube root of 27 is equal to 3.

<strong>Example 2:</strong>
<strong>Input Format:</strong> N = 4, M = 69
<strong>Result:</strong> -1
<strong>Explanation:</strong> The 4th root of 69 does not exist. So, the answer is -1. however 64 with cube root 3 possible.</pre>
<!-- /wp:preformatted -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: O(lon(N))
// SC: O(1)
func getMidMultiply(_ mid: Int, _ n: Int, _ m: Int) ->Int {
    var ans = 1
    for _ in 1...n {
        ans = ans * mid
        if (ans > m) {
            return 2
        }
    }
    if (ans == m) { return 1}// if we got th exact match return as 1 hence we got as a mid element
    return 0
}

func NthRoot(_ n: Int, _ m: Int) ->Int {
    var low = 1
    var high = m
    while low <= high {
        let mid = (low + high) / 2
        let midN = getMidMultiply(mid, n, m)// Find perfect square
        if midN == 1 {// Got perfect square
            return mid
        } else if midN == 0 {// discard first half
            low = mid + 1
        } else {// discard second half
            high = mid - 1
        }
    }
    return -1
}

let firstIp = 3
let secondIp = 27
let opRoot = NthRoot(firstIp, secondIp)
print("The answer is: ", opRoot)// 4 because 3*3*3 = 27</code></pre>
<!-- /wp:code -->