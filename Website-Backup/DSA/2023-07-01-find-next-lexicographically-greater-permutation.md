---
title: "Find next lexicographically greater permutation"
date: 2023-07-01 16:17:27
categories: ['Array-Strings']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/next-permutation/description/" target="_blank" rel="noopener" title="">: </a>A <strong>permutation</strong> of an array of integers is an arrangement of its members into a sequence or linear order.<br>For example, for <code>array = </code>, the following are all the permutations of <code>arr</code>ay: <code>, , , , , </code><br>


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: O(2N)
// SC: O(1)

func nextPermutation(_ nums: inout ) {
    let arrayCount = nums.count
    var lhs = -1, rhs = -1, idx = arrayCount - 2
    while idx >= 0 {
        if nums < nums { lhs = idx; break }
        idx -= 1
    }
    if lhs == -1 { nums = nums.reversed(); return }
    
    idx = arrayCount - 1
    while idx > lhs {
        rhs = idx
        if nums > nums { break }
        idx -= 1
    }
    nums.swapAt(lhs, rhs)
    nums.replaceSubrange(lhs + 1..<arrayCount, with: nums.reversed())
}
var permutationArr = ;
nextPermutation( &permutationArr);
print("The next permutation is: ", permutationArr )// 1,3,2</code></pre>
<!-- /wp:code -->