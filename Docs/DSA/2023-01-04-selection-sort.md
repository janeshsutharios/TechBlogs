---
title: "Selection Sort"
date: 2023-01-04 07:38:54
categories: ['Selection sort in swift', 'Sorting', 'sorting in swift']
layout: post
---

<!-- wp:paragraph -->
Step 1: Find minimum element in array & swap with beginning element <br>Step 2: So now swap min elements from inner loop in the array. 


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: O(n^2)
// SC: O(1)
func selectionSort(_ arr: inout ) {
    
    for i in 0..<arr.count {
        var minIndex = i
        for j in i+1..<arr.count {
            if arr < arr {
                minIndex = j
            }
        }
        arr.swapAt(i, minIndex)
    }
}

var arrayToSort:  = 
selectionSort(&arrayToSort)
print("Sorted Array--> ", arrayToSort)// 
</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
So we have taken `minIndex` which assigned from 0th element i array till last & compare it with i+1 element


<!-- /wp:paragraph -->