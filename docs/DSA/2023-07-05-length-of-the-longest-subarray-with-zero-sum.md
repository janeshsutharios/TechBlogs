---
title: "Length of the longest subarray with zero Sum"
date: 2023-07-05 09:46:48
categories: ['Array-Strings']
layout: post
---

<!-- wp:paragraph -->
<a href="https://takeuforward.org/data-structure/length-of-the-longest-subarray-with-zero-sum/" target="_blank" rel="noopener" title="">: </a><strong>Problem Statement:</strong> Given an array containing both positive and negative integers, we have to find the length of the longest subarray with the sum of all elements equal to zero.<br><strong>Input </strong> array = <br><strong>Result</strong>: 5<br><strong>Explanation</strong>: The following subarrays sum to zero:<br>{-3, 3} , {-1, 6, -5}, {-3, 3, -1, 6, -5}<br>Since we require the length of the longest subarray, answer is <strong>5</strong> 


<!-- /wp:paragraph -->

<!-- wp:heading {"level":6} -->
<h6 class="wp-block-heading"># Approach</h6>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: O(N)
// SC: O(N)
func longestArrayWithNSum(arr: ) -> Int {
    
    var mpp:  =  // Create an dictionary
    var maxi = 0 // longest Subarray found
    var sum = 0 // sum of elements
    
    for i in 0..<arr.count {
        sum += arr
        if (sum == 0) {
            maxi = i + 1
        } else {
            if mpp != nil {
                maxi = max(maxi, i - mpp!)
            } else {
                mpp = i
            }
        }
    }
    return maxi
}

let inputLongestSubArray = 
let outputLongestSubArray = longestArrayWithNSum(arr: inputLongestSubArray)
print("outputLongestSubArray-->", outputLongestSubArray) // 5 which is 10, -3, 3, -1, 6</code></pre>
<!-- /wp:code -->