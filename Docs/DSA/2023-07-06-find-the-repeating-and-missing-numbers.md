---
title: "Find the repeating and missing numbers"
date: 2023-07-06 15:14:37
categories: ['Array-Strings']
layout: post
---

<!-- wp:paragraph -->
<a href="https://www.geeksforgeeks.org/find-a-repeating-and-a-missing-number/" target="_blank" rel="noopener" title="">:</a>Given an unsorted array of size n. Array elements are in the range of 1 to n. One number from set {1, 2, …n} is missing and one number occurs twice in the array. Find these two numbers.<br><strong>Input:</strong> arr = {3, 1, 3}<br><strong>Output:</strong> Missing = 2, Repeating = 3<br><strong>Explanation:</strong> In the array, 2 is missing and 3 occurs twice 


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<strong>Input:</strong> arr = {4, 3, 6, 2, 1, 1}<br><strong>Output:</strong> Missing = 5, Repeating = 1


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">Time Complexity: O(N), where N = the size of the given array.
Reason: We are using only one loop running for N times. So, the time complexity will be O(N).
Space Complexity: O(1)</pre>
<!-- /wp:preformatted -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func findMissingRepeatingNumbers(_ a: ) ->  {
    let n = a.count; // size of the array
    
    // Find Sn and S2n:
    var SN = (n * (n + 1)) / 2;
    var S2N = (n * (n + 1) * (2 * n + 1)) / 6;
    
    // Calculate S and S2:
    var S = 0, S2 = 0;
    for i in 0..<n {
        S += a;
        S2 += a * a;
    }
    
    //S-Sn = X-Y:
    var val1 = S - SN;
    
    // S2-S2n = X^2-Y^2:
    var val2 = S2 - S2N;
    
    //Find X+Y = (X^2-Y^2)/(X-Y):
    val2 = val2 / val1;
    
    //Find X and Y: X = ((X+Y)+(X-Y))/2 and Y = X-(X-Y),
    // Here, X-Y = val1 and X+Y = val2:
    let x = (val1 + val2) / 2;
    let y = x - val1;
    
    return ;
}

var mixArrayForMissingRepeating = ;
var missingAndRepeating = findMissingRepeatingNumbers(mixArrayForMissingRepeating);
print("Misssing & repeating numbers are-->", missingAndRepeating) // </code></pre>
<!-- /wp:code -->