---
title: "How to search an element in Sorted Integer matrix ?"
date: 2023-06-08 03:15:54
categories: ['Array-Strings', 'DSA Swift']
layout: post
---

<!-- wp:paragraph -->
Question : Given an m*<em>n 2D sorted matrix of integers, write a program to find if the given integer exists in the matrix.</em><br>The matrix has the properties below:


<!-- /wp:paragraph -->

<!-- wp:list {"ordered":true} -->
<ol><!-- wp:list-item -->
<li>Integers in each row are sorted from left to right.</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>The first integer of each row is greater than the last integer of the previous row(Increasing order matrix)</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>Column values count is equal for matrix(Symmetric matrix)</li>
<!-- /wp:list-item --></ol>
<!-- /wp:list -->

<!-- wp:paragraph {"textColor":"ast-global-color-1"} -->
<p class="has-ast-global-color-1-color has-text-color"><strong>Approach #1 By removing row and col in each comparisons . Starting from the top right of matrix, move towards the bottom left in search of the target element</strong>


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC O(m+n)
// SC O(1)
func searchMatrix(matrix: ],  target: Int) ->Bool {
    if matrix.isEmpty {
        return false
    }
    var matrixCount = matrix.count
    var matrixRowElementsCount = matrix.count
    var row = 0
    var col = matrixCount - 1
    while row < matrixRowElementsCount && col >= 0 {
        if(matrix == target) {
            return true
        } else if(matrix < target) {
            row = row + 1
        } else {
            col = col - 1
        }
    }
    return false
}

let matrix: ] =
    ,
    ,
    ]
  
let k = 80
print("is element present in matrix", searchMatrix(matrix: matrix, target: k))// true</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph {"textColor":"ast-global-color-1"} -->
<p class="has-ast-global-color-1-color has-text-color"><strong> Approach #2 Binary Search : Considering the matrix as a single array, perform a binary search for the target.</strong>


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">//TC O(log(m*n)) = O(log(m) + log(n))
//SC: O(1)
func searchMatrix2(matrix: ],  target: Int) ->Bool {
    if matrix.isEmpty {
        return false
    }
    var matrixCount = matrix.count
    var matrixRowElementsCount = matrix.count
    var left = 0
    var right = matrixRowElementsCount * matrixCount - 1
    
    while left != right {
        let mid = (left + right - 1) / 2
        if (matrix < target) {
            left = mid + 1
        } else {
            right = mid
        }
    }
    if (matrix == target) {
        return true
    } else {
        return false
    }
}
let matrix: ] =
    ,
    ,
    ]
  
let k = 80
print("is element present in matrix", searchMatrix2(matrix: matrix, target: k))// true</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":6} -->
<h6 class="wp-block-heading">#Approach 2: More use of binary</h6>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">//TC: O(log(m*n))
// SC: O(1)
func searchMatrix(_ matrix: ], _ target: Int) -> Bool {
    if matrix.isEmpty  { return false}
    var lo = 0
    let n = matrix.count
    let m = matrix.count
    var hi = (n * m) - 1
    
    while lo <= hi {
        var  mid = (lo + (hi - lo) / 2)
        if matrix == target {
            return true
        }
        if matrix < target {
            lo = mid + 1
        } else {
            hi = mid - 1
        }
    }
    return false
}

let matrixSorted = ,
                    ,
                    ]
let elementToSearch = 3
let isFoundInMatrix = searchMatrix(matrixSorted, elementToSearch)
print("is FoundInMatrix ", isFoundInMatrix)// true</code></pre>
<!-- /wp:code -->