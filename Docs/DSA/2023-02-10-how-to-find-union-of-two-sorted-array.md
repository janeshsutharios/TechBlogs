---
title: "How to find union of two sorted array ?"
date: 2023-02-10 10:27:08
categories: ['Array-Strings', 'DSA Swift', 'union of two arrays']
layout: post
---

<!-- wp:paragraph -->
: In a given two sorted array find union elements. Output should be sorted. <br>For example :  arr1 = {1,2,3,4,5}  arr2 = {2,3,4,4,5} Output:  {1,2,3,4,5}<br><strong>Approach #1</strong>: Use Dictionary / Hashset & after it sort the array which SC: O(m+n) TC: <strong>O( (m+n)log(m+n) </strong>) <br><strong>Approach #2</strong>: Two pointer approach: use two pointer i & j & fill the elements if first array index is lesser fill it first otherwise fill from another array


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func unionOfTwoSortedArray(array1: , array2: ) ->  {
    let firstLength = array1.count
    let secondLength = array2.count
    var i = 0, j = 0
    var unionArray:  = 
    
    while i < firstLength && j < secondLength {
        if array1 < array2 {
            // To check if unionArray is non empty & elements is not present already
            if unionArray.isEmpty || unionArray.last != array1 {
                unionArray.append(array1)
            }
            i+=1
        } else {
            if unionArray.isEmpty || unionArray.last != array2 {
                unionArray.append(array2)
            }
            j+=1
        }
    }
    while i < firstLength {
        if unionArray.last != array1 {
            unionArray.append(array1)
        }
        i+=1
    }
    while j < secondLength {
        if unionArray.last != array2 {
            unionArray.append(array2)
        }
        j+=1
    }
    return unionArray
}

let firstArray = 
let secondArray = 

let unionArray = unionOfTwoSortedArray(array1: firstArray, array2: secondArray)
print("union-Array->", unionArray)// O/P: </code></pre>
<!-- /wp:code -->