---
title: "Rotate array matrix by 90 degree"
date: 2023-07-01 14:38:00
categories: ['Array-Strings']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/rotate-image/description/" target="_blank" rel="noopener" title=""> :</a> Given a 2D matrix, your task is to rotate the matrix 90 degrees clockwise.<br>Input: -  , , ]<br>Output -  , , ]


<!-- /wp:paragraph -->

<!-- wp:image {"id":1859,"sizeSlug":"full","linkDestination":"none"} -->
<figure class="wp-block-image size-full">![](/TechBlogs/Assets/Website/2023/07/matrix.jpeg)</figure>
<!-- /wp:image -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func rotateMatrix(_ matrix: inout ]) {
    var rows = matrix.count
    var columns = rows
    
    //transpose of Matrix
    for row in 0..<rows {
        for column in row..<columns {
            let temp = matrix
            matrix = matrix
            matrix = temp
        }
    }
    
    for row in 0..<rows {
        matrix.reverse()
    }
}

var matrixToRotate =  , , ]
rotateMatrix(&matrixToRotate);
print("Rotated matrix output-->", matrixToRotate)//  , , ]</code></pre>
<!-- /wp:code -->