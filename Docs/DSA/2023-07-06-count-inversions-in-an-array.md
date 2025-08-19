---
title: "Count inversions in an array"
date: 2023-07-06 15:25:17
categories: ['Array-Strings']
layout: post
---

<!-- wp:paragraph -->
<a href="https://takeuforward.org/data-structure/count-inversions-in-an-array/" target="_blank" rel="noopener" title="">: </a>Given an array of N integers, count the inversion of the array (using <a href="https://takeuforward.org/data-structure/merge-sort-algorithm/" target="_blank" rel="noreferrer noopener">merge-sort</a>). What is an inversion of an array? Definition: for all i & j < size of array, if i < j then you have to find pair (A,A) such that A < A.<br><strong>Example 1:</strong><br><strong>Input Format</strong>: N = 5, array = {1,2,3,4,5}<br><strong>Result</strong>: 0<br><strong>Explanation</strong>: we have a sorted array and the sorted array has 0 inversions as for i < j you will never find a pair such that A < A. More clear example: 2 has index 1 and 5 has index 4 now 1 < 5 but 2 < 5 so this is not an inversion.<br><br><strong>Example 2:</strong><br><strong>Input Format</strong>: N = 5, array = {5,4,3,2,1}<br><strong>Result</strong>: 10<br><strong>Explanation</strong>: we have a reverse sorted array and we will get the maximum inversions as for i < j we will always find a pair such that A < A. Example: 5 has index 0 and 3 has index 2 now (5,3) pair is inversion as 0 < 2 and 5 > 3 which will satisfy out conditions and for reverse sorted array we will get maximum inversions and that is (n)*(n-1) / 2.For above given array there is 4 + 3 + 2 + 1 = 10 inversions.<br><br><strong>Example 3:</strong><br><strong>Input Format</strong>: N = 5, array = {5,3,2,1,4}<br><strong>Result</strong>: 7<br><strong>Explanation</strong>: There are 7 pairs (5,1), (5,3), (5,2), (5,4),(3,2), (3,1), (2,1) and we have left 2 pairs (2,4) and (1,4) as both are not satisfy our condition. <br>


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
Time Complexity: O(N*logN), where N = size of the given array.<br>Reason: We are not changing the merge sort algorithm except by adding a variable to it. So, the time complexity is as same as the merge sort.<br>Space Complexity: O(N),


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func numberOfInversions(_ arr: ) -> Int {
    var cnt = 0
    for i in 0..<arr.count {
        for j in i..<arr.count {
            if arr > arr {
                cnt+=1
            }
        }
    }
    return cnt
}

let conversionArrayInput = 
let conversionArrayOutput = numberOfInversions(conversionArrayInput)
print("The number of inversions is: ", conversionArrayOutput) // 10</code></pre>
<!-- /wp:code -->