---
title: "Get Spiral Traversal of Matrix"
date: 2023-07-01 16:03:36
categories: ['Array-Strings']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/spiral-matrix/description/" target="_blank" rel="noopener" title="">: </a><strong> </strong>Given a Matrix, print the given matrix in spiral order.<br><strong>Input:</strong> matrix = ,,] <br><strong>Output:</strong> 


<!-- /wp:paragraph -->

<!-- wp:image {"id":1863,"sizeSlug":"full","linkDestination":"none"} -->
<figure class="wp-block-image size-full">![](/TechBlogs/Assets/Website/2023/07/spiral1.jpg)</figure>
<!-- /wp:image -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: O(MxN)
// TC: O(N)
func spiralOrder(_ matrix: ]) ->  {
    if matrix.isEmpty { return  }
    
    var result:  = 
    var rBegin = 0, rEnd = matrix.count - 1
    var cBegin = 0, cEnd = matrix.count - 1
    
    while rBegin <= rEnd && cBegin <= cEnd {
        // Traverse right
        for i in stride(from: cBegin, to: cEnd + 1, by: 1) {
            result.append(matrix)
        }
        rBegin += 1
        
        // Traverse down
        for i in stride(from: rBegin, to: rEnd + 1, by: 1) {
            result.append(matrix)
        }
        cEnd -= 1
        
        // Traverse left
        if rBegin <= rEnd {
            for i in stride(from: cEnd, to: cBegin - 1, by: -1) {
                result.append(matrix)
            }
        }
        rEnd -= 1
        
        // Traverse up
        if cBegin <= cEnd {
            for i in stride(from: rEnd, to: rBegin - 1, by: -1) {
                result.append(matrix)
            }
        }
        cBegin += 1
    }
    return result
}
var spiralMatrix =  , , ]
print("spiralMatrix matrix output-->", spiralOrder(spiralMatrix))//  </code></pre>
<!-- /wp:code -->