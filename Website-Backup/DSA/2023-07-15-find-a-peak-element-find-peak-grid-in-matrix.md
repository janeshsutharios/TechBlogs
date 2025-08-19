---
title: "Find a Peak Element (Find Peak Grid in Matrix)"
date: 2023-07-15 09:18:48
categories: ['BinarySearch']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/find-a-peak-element-ii/description/" target="_blank" rel="noopener" title="">:</a> A <strong>peak</strong> element in a 2D matrix is an element that is <strong>strictly greater</strong> than all of its <strong>adjacent </strong>neighbour's to the left, right, top, and bottom.


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
Given a <strong>0-indexed</strong> <code>m x n</code> matrix  <code>mat</code> where <strong>no two adjacent cells are equal</strong>, find <strong>any</strong> peak element <code>mat</code> and return <em>the length 2 array </em><code></code>.You may assume that the entire matrix is surrounded by an <strong>outer perimeter</strong> with the value <code>-1</code> in each cell.


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
Write an algorithm that runs in <code>O(m log(n))</code> or <code>O(n log(m))</code> time. Some examples are below


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Input:</strong> mat = ,]
<strong>Output:</strong> 
<strong>Explanation:</strong> Both 3 and 4 are peak elements so  and  are both acceptable answers.
Input: mat = ,,]
Output: 
Explanation: Both 30 and 32 are peak elements so  and  are both acceptable answers.</pre>
<!-- /wp:preformatted -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: M*log(N).
// SC: O(1)
func findPeakGrid(_ mat: ]) ->  {
    var startCol = 0, endCol = mat.count-1
    
    while startCol <= endCol {
        var maxRow = 0, midCol = startCol + (endCol-startCol)/2
        
        for row in 0..<mat.count {
            maxRow = mat >= mat ? row : maxRow
        }
        
        var leftIsBig    =   midCol-1 >= startCol  &&  mat > mat
        var rightIsBig   =   midCol+1 <= endCol    &&  mat > mat
        
        if !leftIsBig && !rightIsBig {  // we have found the peak element
            return 
            
        } else if (rightIsBig) { // if rightIsBig, then there is an element in 'right' that is bigger than all the elements in the 'midCol',
            startCol = midCol+1 //so 'midCol' cannot have a 'peakPlane'
            
        } else  {// leftIsBig
            endCol = midCol-1
        }
    }
    return 
}

let demoMatrix = ,,]
let peakElement = findPeakGrid(demoMatrix)
print("Peak Grid is--- ", peakElement)// // Explanation: Both 30 and 32 are peak elements so  and  are both acceptable answers.</code></pre>
<!-- /wp:code -->