---
title: "How to find subset sum"
date: 2022-11-23 12:59:57
categories: ['DSA', 'Recursion', 'subset sums']
layout: post
---

<!-- wp:paragraph -->
<a href="https://practice.geeksforgeeks.org/problems/subset-sums2234/1" target="_blank" rel="noopener" title=""></a> : Find subset sum in given Array<br>Example: Input: N = 6 arr = {3, 34, 4, 12, 5, 2} sum = 9 Output: 1 Explanation: Here there exists a subset with sum = 9, 4+3+2 = 9.


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func sumSubSet(ind: Int, sum: Int, op: inout , inArray: ,n: Int) {
    if ind == n {
        op.append(sum)
        return
    }
    // Pick An Element
    sumSubSet(ind: ind+1, sum: sum+inArray, op: &op, inArray: inArray, n: n)
    // Not Pick An Element
    sumSubSet(ind: ind+1, sum: sum, op: &op, inArray: inArray, n: n)
}


//Input: candidates = , target = 8
let inArray = 
var op:  = 
let n = 2
sumSubSet(ind: 0, sum: 0, op: &op, inArray: inArray, n: n)
print(op.sorted())</code></pre>
<!-- /wp:code -->