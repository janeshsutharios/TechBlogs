---
title: "Find out how many times the array has been rotated || Find Lowest Element Index"
date: 2023-07-09 16:42:35
categories: ['BinarySearch']
layout: post
---

<!-- wp:paragraph -->
<a href="https://takeuforward.org/arrays/find-out-how-many-times-the-array-has-been-rotated/" target="_blank" rel="noopener" title="">  </a>Given an integer array <strong>arr</strong> of size <strong>N</strong>, sorted in ascending order (<strong>with distinct values</strong>). Now the array is rotated between 1 to N times which is unknown. Find how many times the array has been rotated. <br>


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Example 1:</strong>
<strong>Input Format:</strong> arr = 
<strong>Result:</strong> 4
<strong>Explanation:</strong> The original array should be . So, we can notice that the array has been rotated 4 times.</pre>
<!-- /wp:preformatted -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: O(log(N))
// SC: O(1)
func findLowestNumberIndex(_ nums: ) ->Int {
    
    var low = 0
    var high = nums.count - 1
    var ans = Int.max
    var index = -1
    while low <= high {
        let mid = (low + high) / 2
        //search space is already sorted
        //then arr will always be
        //the minimum in that search space:
        if nums <= nums {
            if nums < ans {
                index = low
                ans = nums
            }
            break
        }
        
        // If left part is sorted:
        if nums <= nums {
            // Keep the minimum:
            if nums < ans {
                index = low
                ans = nums
            }

            // Eliminate left half:
            low = mid + 1
        } else { // If right part is sorted:
            // Keep the minimum:
            if nums < ans {
                index = mid
                ans = nums
            }

            // Eliminate right half:
            high = mid - 1
        }
    }
    return index
}

let rotaArrayInput = 
let rotaArrayOutput = findLowestNumberIndex(rotaArrayInput)
print("The minimum element index is: ", rotaArrayOutput)// 4</code></pre>
<!-- /wp:code -->