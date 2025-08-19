---
title: "Set Matrix Zeroes in swift"
date: 2022-11-01 10:45:47
categories: ['Array-Strings', 'DSA', 'DSA Swift', 'matrix questions in Swift']
layout: post
---

<!-- wp:paragraph -->
Question: - if on given matrix any element is zero set entire row & column to zero 


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func setZeroes(_ matrix: inout ]) {
    //Approach 2
    
    var matrixCount = matrix.count;
    var firstRowCount = matrix.count;
    var isCol = false
    for rowIndex in 0..<matrixCount {
        if matrix == 0 {
            isCol = true
        }
        
        for colIndex in 1..<firstRowCount {
            if matrix == 0 {
                matrix = 0
                matrix = 0
            }
        }
    }
    
    for rowIndex in 1..<matrixCount {
        for colIndex in 1..<firstRowCount {
            if (matrix == 0) || ((matrix == 0)) {
                matrix = 0
            }
        }
    }
    
    if matrix == 0 {
        for colIndex in 0..<firstRowCount {
            // Making cols to zero
            matrix = 0
        }
    }
    
    if isCol {
        for rowIndex in 0..<matrixCount {
            // Making rows to zero
            matrix = 0
        }
    }
    
}
var matrixValue = ,,]
setZeroes(&matrixValue)
print(matrixValue)
//Input: matrix = ,,]
//Output: ,,]
</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":5} -->
<h5 class="wp-block-heading">Approach #2</h5>
<!-- /wp:heading -->

<!-- wp:paragraph -->
 Here we find the rows & cols which is zero & then iterate over matrix & make that rows and cols as zero


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// Time Complexity: O(M×N) where M and N are the number of rows and columns respectively.
// Space Complexity: O(M + N).
// This is taking extra space because of storage of rows & cols.
func setZeroes(_ matrix: inout ]) {
    
    var cacheRows:  = 
    var cacheCols:  = 
    
    for i in 0..<matrix.count {
        for j in 0..<matrix.count {
            // Set Rows Cols index cache
            if matrix == 0 {
                cacheRows.append(i)
                cacheCols.append(j)
            }
        }
    }
    
    
    for i in 0..<matrix.count {
        for j in 0..<matrix.count {
            // Set matrix to zero where it contains i Row & j Col
            if cacheRows.contains(i) || cacheCols.contains(j) {
                matrix = 0
            }
        }
    }
}
var matrixArr1 = ,,]
var matrixArr2 = ,,]
setZeroes(&matrixArr1)
setZeroes(&matrixArr2)
print("matrix1 array-->", matrixArr1) // , , ]
print("matrix2 array-->", matrixArr2) // , , ]</code></pre>
<!-- /wp:code -->