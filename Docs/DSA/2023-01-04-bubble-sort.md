---
title: "Bubble sort."
date: 2023-01-04 11:13:05
categories: ['bubble sort in swift', 'Sorting', 'sorting in swift']
layout: post
---

<!-- wp:paragraph -->
Approach: Swap Adjacent elements from an array a > a then swap 


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: O(n^2)
// SC: O(1)
func bubbleSort(_ arr: inout ) {
    for i in 0..<arr.count-1 {
        for j in 0..<arr.count-i-1 {
            if arr > arr {
                arr.swapAt(j, j+1)
            }
        }
    }
}
var arrayToSort:  = 
bubbleSort(&arrayToSort)
print("Sorted Array--> ", arrayToSort)// </code></pre>
<!-- /wp:code -->