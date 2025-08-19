---
title: "Find Ceil & Floor element in an array"
date: 2023-07-08 12:37:40
categories: ['BinarySearch']
layout: post
---

<!-- wp:paragraph -->
<a href="https://takeuforward.org/arrays/floor-and-ceil-in-sorted-array/" target="_blank" rel="noopener" title="">: </a>You’re given an sorted array arr of n integers and an integer x. Find the floor and ceiling of x <br>The floor of x is the largest element in the array which is smaller than or equal to x.<br>The ceiling of x is the smallest element in the array greater than or equal to x.<br>We will use Binary Search here


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: O(log(N))
// SC: O(1)
func findCeil(_ arr: , _ targetElement: Int) -> Int {
    let arrayCount = arr.count
    var low = 0
    var high = arrayCount - 1
    var ans = arrayCount//So if element is greater it would be the last
    
    while low <= high {
        let mid = (low + high) / 2
        // maybe an answer
        if arr >= targetElement {
            ans = arr
            // look for smaller index on the left
            high = mid - 1
        } else {
            low = mid + 1 // look on the right
        }
    }
    return ans
}

func findFloor(_ arr: , _ targetElement: Int) -> Int {
    let arrayCount = arr.count
    var low = 0
    var high = arrayCount - 1
    var ans = arrayCount//So if element is greater it would be the last
    
    while low <= high {
        let mid = (low + high) / 2
        // maybe an answer
        if arr <= targetElement {
            ans = arr
            // look for smaller index on the left
            low = mid + 1 // look on the right
        } else {
            high = mid - 1; // look on the right
        }
    }
    return ans
}

var inputBinaryArray = 
let targetEl = 5
let floorFound = findFloor(inputBinaryArray, targetEl)
let ceilFound = findCeil(inputBinaryArray, targetEl)

print("floorFound ", floorFound) // 4
print("ceilFound ", ceilFound) // 7</code></pre>
<!-- /wp:code -->