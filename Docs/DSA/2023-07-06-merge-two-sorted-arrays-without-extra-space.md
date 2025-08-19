---
title: "Merge two Sorted Arrays Without Extra Space"
date: 2023-07-06 12:27:20
categories: ['Array-Strings']
layout: post
---

<!-- wp:paragraph -->
<a href="https://practice.geeksforgeeks.org/problems/merge-two-sorted-arrays-1587115620/1?company=Synopsys&company=Synopsys&page=1&query=companySynopsyspage1companySynopsys&utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=merge-two-sorted-arrays" target="_blank" rel="noopener" title="">: </a>Given two sorted arrays <strong>arr1</strong> and <strong>arr2 </strong>ofsizes <strong>n</strong> and <strong>m</strong> in non-decreasing order. Merge them in sorted order without using any extra space. Modify arr1 so that it contains the first N elements and modify arr2 so that it contains the last M elements.<br>


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<strong>Example 1:</strong>


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Input</strong>: 
n = 4, arr1 =  
m = 5, arr2 = 
<strong>Output</strong>: 
arr1 = 
arr2 = 
<strong>Explanation</strong>:
After merging the two 
non-decreasing arrays, we get, 
0 1 2 3 5 6 7 8 9.</pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<strong>Example 2:</strong>


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Input</strong>: 
n = 2, arr1 =  
m = 3, arr2 = 
<strong>Output</strong>: 
arr1 = 
arr2 = 
<strong>Explanation</strong>:
After merging two sorted arrays 
we get 5 10 12 18 20.</pre>
<!-- /wp:preformatted -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">/**
 Time Complexity: O((n+m)*log(n+m)), where n and m are the sizes of the given arrays.
 Reason: The gap is ranging from n+m to 1 and every time the gap gets divided by 2. So, the time complexity of the outer loop will be O(log(n+m)). Now, for each value of the gap, the inner loop can at most run for (n+m) times. So, the time complexity of the inner loop will be O(n+m). So, the overall time complexity will be O((n+m)*log(n+m)).

 Space Complexity: O(1) as we are not using any extra space.
 */
func mergeTowSortedArrays(_ arr1: inout , _ arr2: inout , _ n: Int, _ m: Int) {
    
    var len = n + m
    var gap = len / 2
    
    while gap > 0 {
        var left = 0
        var right = left + gap
        
        while right < len {
            if left < n && right >= n {
                swapIfGreater(&arr1, &arr2, left, right - n)
            } else if left >= n {
                var newArr2 = arr2
                swapIfGreater(&arr2, &newArr2, left - n, right - n)
            } else {
                var newArr1 = arr1
                swapIfGreater(&arr1, &newArr1, left, right)
            }
            left += 1
            right+=1
        }
        
        if gap == 1 { break }
        
        gap = (gap / 2) + (gap % 2)

    }
    
    func swapIfGreater(_ arr1: inout , _ arr2: inout , _ ind1: Int, _ ind2: Int) {
        if arr1 > arr2 {
            (arr1, arr2) = (arr2, arr1)
        }
    }
}

var arr1 = 
var arr2 = 
var n = 4, m = 3

mergeTowSortedArrays(&arr1, &arr2, n, m)

print("The merged arrays are:--", arr1, arr2)//  </code></pre>
<!-- /wp:code -->