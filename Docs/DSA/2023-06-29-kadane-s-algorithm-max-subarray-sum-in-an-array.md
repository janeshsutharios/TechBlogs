---
title: "Kadane's Algorithm: Max subarray sum in an array"
date: 2023-06-29 12:38:28
categories: ['Array-Strings']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/maximum-subarray/" target="_blank" rel="noopener" title="">:</a> Find max sum in an given array 


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func findSubArrayWithMaxSumKadane(arr: inout ) -> (sumValue: Int, startIndex: Int, endIndex: Int) {
 
    var sum = 0
    var maximumValue = 0
    
    // variables to capture start and end index
    var startIndex = 0
    var endIndex = 0
    var progressiveStartIndex = 0
    //
    
    for i in 0..<arr.count {
        sum += arr
        if sum > maximumValue {
            maximumValue = sum
            startIndex = progressiveStartIndex
            endIndex = i
        }
        if sum < 0 {
            sum = 0
            progressiveStartIndex = i+1
        }
    }
    return (sumValue: maximumValue, startIndex: startIndex, endIndex: endIndex)
}

var kadaneArray = 
let kadaneSum = findSubArrayWithMaxSumKadane(arr: &kadaneArray)
print("The kadaneSum  is:", kadaneSum)</code></pre>
<!-- /wp:code -->