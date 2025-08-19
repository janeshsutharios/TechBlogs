---
title: "Find missing number from first N natural numbers."
date: 2023-06-05 06:57:41
categories: ['Array-Strings', 'DSA Swift']
layout: post
---

<!-- wp:paragraph -->
Question:  Find the missing number in first n Natural numbers...


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// Approach 1: Using Summation
// TC:O(n)
// SC:O(1)
func findMissingNumber1(arr: ) ->Int {
    let len = arr.count + 1
    var summationOfFirstN = len*(len+1)/2
    for value in arr {
        summationOfFirstN -= value
    }
    return summationOfFirstN
}

// Approach 2: Using Summation
// TC:O(n)
// SC:O(1)
//To avoid integer overflow, pick one number from the range  and subtract a number from the given array (don’t subtract the same number twice)

func findMissingNumber2(arr: ) ->Int {
    var total: Int = 1
    var arrCount = arr.count + 1
 
    for i in 2..<arrCount {
        total += i;
        total = total - arr;
    }
    return total;
}

// Approach 3: Using XOR
// TC:O(2n)
// SC:O(1)
func findMissingNumber3(arr: ) ->Int {

    var arrCount = arr.count
    // For xor of all the elements in array
    var x1 = arr;
 
    // For xor of all the elements from 1 to n+1
    var x2 = 1;
 
    for i in 1..<arrCount-1 {
        x1 = x1 ^ arr
    }
    for i in 2..<arrCount+1 {
        x2 = x2 ^ i
    }
    return x1 ^ x2
}
 var arrayMiss:  = 
print("Missing numbers is-->", findMissingNumber1(arr: arrayMiss))// 4
print("Missing numbers is-->", findMissingNumber2(arr: arrayMiss))// 4
print("Missing numbers is-->", findMissingNumber3(arr: arrayMiss))//4</code></pre>
<!-- /wp:code -->