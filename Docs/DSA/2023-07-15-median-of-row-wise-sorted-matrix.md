---
title: "Median of Row Wise Sorted Matrix"
date: 2023-07-15 09:37:58
categories: ['BinarySearch']
layout: post
---

<!-- wp:paragraph -->
: Given a row-wise sorted matrix of size r*c, where r is no. of rows and c is no. of columns, find the median in the given matrix. <strong>where </strong>– r*c is odd


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Example 1:</strong>
<strong>Input:</strong> 
r = 3 , c = 3
1 4 9 
2 5 6
3 8 7
<strong>Output:</strong> Median = 5
<strong>Explanation:</strong> If we find the linear sorted array, the array becomes 1 2 3 4 5 6 7 8 9
So, median = 5

<strong>Example 2:</strong>
<strong>Input:</strong> 
r = 3 , c = 3
1 3 8
2 3 4
1 2 5
<strong>Output:</strong> Median = 3
<strong>Explanation:</strong> If we find the linear sorted array, the array becomes 1 1 2 2 3 3 4 5 7 8
So, median = 3</pre>
<!-- /wp:preformatted -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC:O(row*log col)
// SC:O(1)
func countSmallerThanMid(_ A: , _ mid: Int,_ n: Int) ->Int {
    var l = 0, h = n - 1
    while l <= h {
        var md = (l + h) >> 1
        if (A <= mid) {
            l = md + 1
        } else {
            h = md - 1
        }
    }
    return l
}

func findMedian(_ A: ], _ row: Int, _ col: Int) -> Int {
    var low = 1
    var high = 1000000000
    var n = row
    var m = col
    while low <= high {
        var mid = (low + high) >> 1
        var cnt = 0
        for i in 0..<n {
            cnt += countSmallerThanMid(A, mid, col)
        }
        if (cnt <= (n * m) / 2) {
            low = mid + 1
        } else {
            high = mid - 1
        }
    }
    return low
}
var row1 = 3, col1 = 3
var aMatrix = ,
           ,
           ]
print("The median of the row-wise sorted matrix is: ", findMedian(aMatrix, row1, col1)) // 3
//Explanation: If we find the linear sorted array, the array becomes 1 1 2 2 3 3 4 5 7 8 So, median = 3</code></pre>
<!-- /wp:code -->