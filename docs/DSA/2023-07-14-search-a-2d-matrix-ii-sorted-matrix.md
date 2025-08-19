---
title: "Search a 2D Matrix II (Sorted Matrix)"
date: 2023-07-14 16:08:23
categories: ['BinarySearch']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/search-a-2d-matrix-ii/description/" target="_blank" rel="noopener" title=""> :</a> Write an efficient algorithm that searches for a value <code>target</code> in an <code>m x n</code> integer matrix <code>matrix</code>. This matrix has the following properties:


<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><!-- wp:list-item -->
<li>Integers in each row are sorted in ascending from left to right.</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>Integers in each column are sorted in ascending from top to bottom.</li>
<!-- /wp:list-item --></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<strong>Example 1:</strong>


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Input:</strong> matrix = ,,,,], target = 5
<strong>Output:</strong> true</pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<strong><em>Why Binary Search is not useful for searching in unsorted arrays?</em></strong>


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
The basic condition to apply Binary Search anywhere in any algorithm is that the search space should be sorted. To perform a Binary search in the 2D array, the array needs to be sorted. Here is an unsorted 2D array is given, so applying Binary Search in an unsorted array is not possible. To apply Binary Search first the 2D array needs to be sorted in any order that itself takes<strong> (M*N)log(M*N)</strong> time. So the total time complexity to search any element here is <strong>O((M * N) log(M * N)) + O(N + M)</strong> which very poor when it is compared with the time complexity of Linear Search which is just <strong>O(N*M)</strong>. Therefore, Linear Search is used for searching in an unsorted array, not Binary Search.


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
Below is the implementation for Binary search in 2D arrays:


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: O(N + M)
// SC: O(1)
func searchMatrix2(_ matrix: ], _ target: Int) -> Bool {
    var row = 0;
    var col = matrix.count - 1;
    while row < matrix.count && col >= 0 {
        if matrix == target {
            return true// row, col
        }
        if matrix < target {
            row+=1 // Target lies in further row
        } else {
            col-=1  // Target lies in previous column
        }
    }
    return false
}
let searchMatrix = ,,,,]
let targetToSearch = 5
let opSearchElement = searchMatrix2(searchMatrix, targetToSearch)
print(" opSearchElement --- ", opSearchElement)// true</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
<strong>Improved Binary Search in a 2D Array: </strong>


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
We can reduce the time by converting 2D array to 1D array. Add row one after another and search the item then convert it to 2D again.


<!-- /wp:paragraph -->

<!-- wp:table -->
<figure class="wp-block-table"><table><tbody><tr><td>1</td><td>2</td><td>3</td></tr><tr><td>4</td><td>5</td><td>6</td></tr><tr><td>7</td><td>8</td><td>9</td></tr></tbody></table></figure>
<!-- /wp:table -->

<!-- wp:paragraph -->
Convert it to 1D array 


<!-- /wp:paragraph -->

<!-- wp:table -->
<figure class="wp-block-table"><table><tbody><tr><td>1</td><td>2</td><td>3</td><td>4</td><td>5</td><td>6</td><td>7</td><td>8</td><td>9</td></tr></tbody></table></figure>
<!-- /wp:table -->

<!-- wp:paragraph -->
Now apply normal binary search and get the result. Not necessary store the 1D in new array you can create it virtually by converting row, col value to 1D index vice-versa 1D to row, col value.   


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// Approch 2: by converring it into 1D matrix.
// TC: O(log N*M)
// SC: O(1)
func searchMatrix2Using1D(_ matrix: ], _ target: Int) -> Bool {
    var row = matrix.count
    var col = matrix.count
    var l = 0, h = row * col - 1
    while (l <= h) {
        let mid = l + ((h - l) / 2)
        let tC = mid % col
        let tR = (mid / col)
        let val = matrix
        if (val == target){
            return true
        }
        if (val < target) {
            l = mid + 1
        } else {
            h = mid - 1
        }
    }
    return false
}</code></pre>
<!-- /wp:code -->