---
title: "How to find intersection of two sorted array"
date: 2023-02-10 11:08:51
categories: ['Array-Strings', 'intersection of two arrays']
layout: post
---

<!-- wp:paragraph -->
 In given two sorted arrays find intersection.<br>// Ex-->    A:  , B:  Output: 3,3,5<br>#Approach: // TC O(n) // SC O(1)


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func findIntersactionOfElements(array1: , array2: ) ->  {
    let firstLength = array1.count
    let secondLength = array2.count
    var i = 0, j = 0
    var intersactionArray:  = 
    
    while i < firstLength && j < secondLength {
        // Intersaction means elements are equal so we just compare i & j
        if array1 == array2 {
            intersactionArray.append(array1)
            i+=1
            j+=1
        } else  if array1 < array2 {
            i+=1
        } else  {
            j+=1
        }
    }
            
    return intersactionArray
}
let firstArray = 
let secondArray = 

let intersactionArray = findIntersactionOfElements(array1: firstArray, array2: secondArray)
print("intersactionArray-Array->", intersactionArray)
</code></pre>
<!-- /wp:code -->