---
title: "Find the row with maximum number of 1s"
date: 2023-07-14 10:45:32
categories: ['BinarySearch']
layout: post
---

<!-- wp:paragraph -->
<a href="https://www.geeksforgeeks.org/find-the-row-with-maximum-number-1s/" target="_blank" rel="noopener" title="">: </a>Given a boolean 2D array, where each row is sorted. Find the row with the maximum number of 1s. 


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func rowWithMax1s(_ mat: ]) ->Int {
    
    let row = 4
    let col = 4
    // Initialize first row as row with max 1s
    var maxRowIndex = 0;
    var j = col - 1;
    
    for i in  0..<row {
        // Move left until a 0 is found
        var flag = false
        
        // to check whether a row has more 1's than previous
        while j >= 0 && mat == 1 {
            
            j = j - 1; // Update the index of leftmost 1
            // seen so far
            flag = true;//present row has more 1's than previous
        }
        
        // if the present row has more 1's than previous
        if flag {
            maxRowIndex = i; // Update max_row_index
        }
    }
    if maxRowIndex == 0 && mat == 0 {
        return -1;
    }
    return maxRowIndex;
}

// Driver Code
let oncesMatric = ,
                   ,
                   ,
                   ];

print("Index of row with maximum 1s is ", rowWithMax1s(oncesMatric))// 2</code></pre>
<!-- /wp:code -->