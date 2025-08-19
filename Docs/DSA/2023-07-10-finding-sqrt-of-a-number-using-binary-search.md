---
title: "Finding Sqrt of a number using Binary Search"
date: 2023-07-10 06:35:35
categories: ['BinarySearch']
layout: post
---

<!-- wp:paragraph -->
<a href="https://takeuforward.org/binary-search/finding-sqrt-of-a-number-using-binary-search/" target="_blank" rel="noopener" title="">:</a> Find SQRT of a number using binary search.<br>Example: <strong>Input:</strong> x = 8.  <strong>Output:</strong> 2


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: O(lon(N))
// SC: O(1)
func findSQRT(_ n: Int) ->Int {
    var low = 1
    var high = n;
    // Binary search on the answers:
    while low <= high {
        let mid = ((low + high) / 2)
        let val = mid * mid
        if (val <= n) {
            // Eliminate the left half:
            low = mid + 1
        } else {
            // Eliminate the right half:
            high = mid - 1
        }
    }
    return high
}   
let inputSQRT = 16
let opSQRT = findSQRT(inputSQRT)
print("opSQRT is --- ", opSQRT) //opSQRT 4</code></pre>
<!-- /wp:code -->