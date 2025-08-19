---
title: "Count the number of subarrays with given xor K"
date: 2023-07-06 09:30:57
categories: ['Array-Strings']
layout: post
---

<!-- wp:paragraph -->
<a href="https://takeuforward.org/data-structure/count-the-number-of-subarrays-with-given-xor-k/" target="_blank" rel="noopener" title="">:</a> <strong>Problem Statement:</strong> Given an array of integers A and an integer B. Find the total number of subarrays having bitwise XOR of all elements equal to k.<br><strong>Example 1:</strong><br><strong>Input Format:</strong> A =  , k = 6<br><strong>Result:</strong> 4<br><strong>Explanation:</strong> The subarrays having XOR of their elements as 6 are  , , , 


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: O(N)
// SC: O(N)
// Question SumWithXor
func subarraysWithXorK(_ arr: , _ k: Int) ->Int {
    let arrCount = arr.count; //size of the given array.
    var xr = 0;
    var mpp: = 
    mpp = 1 //setting the value of 0.
    var cnt = 0;
    
    for i in 0..<arrCount {
        // prefix XOR till index i:
        xr = xr ^ arr;
        
        //By formula: x = xr^k:
        let x = xr ^ k;
        
        // add the occurrence of xr^k
        // to the count:
        cnt += mpp

        // Insert the prefix xor till index i
        // into the map:
        mpp = mpp + 1
    }
    return cnt
}

let xorArray = 
let kValue = 5;
print("subarraysWithXorK ---  ", subarraysWithXorK(xorArray, kValue))// 2</code></pre>
<!-- /wp:code -->