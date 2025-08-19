---
title: "Two Sum Problem"
date: 2023-06-29 11:35:12
categories: ['Array-Strings', 'two-sum']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/two-sum/" target="_blank" rel="noopener" title=""> :</a> Given an array of integers <code>nums</code> and an integer <code>target</code>, find <em>indices of the two numbers</em> which addition equals to target.<br>Example: Input: nums = , target = 13 Output:  Explanation: Because nums + nums == 13, we return .


<!-- /wp:paragraph -->

<!-- wp:heading {"level":6} -->
<h6 class="wp-block-heading">Approach #1 : Using Two pointers: - </h6>
<!-- /wp:heading -->

<!-- wp:paragraph -->
Step 1: First sort array then<br>Step 2: If arr + arr > sum, we will decrement the right pointer.<br>Step 3: If arr + arr < sum, we will increment the left pointer.<br>Step 4: if arr + arr == sum, we will return the result.


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: O(N)
// SC: O(1)
func twoSum(arr: inout , target: Int) -> {
    arr.sort()
    var left = 0
    var right = arr.count - 1
    while (left < right) {
        let sum = arr + arr
        if (sum == target) {
            return 
        } else if sum < target {
            left+=1
        } else {
            right-=1
        }
    }
    return 
}

var twoSumArr = 
let target = 14
let ans = twoSum(arr: &twoSumArr, target: target)
print("two sum index found-->", ans, twoSumArr], twoSumArr])</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":6} -->
<h6 class="wp-block-heading">Approach#2 : Using Map/Dictionary</h6>
<!-- /wp:heading -->

<!-- wp:paragraph -->
Since dictionary contains Unique keys we are storing elements to dictionary & when target-element is sum we are returning index.


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func twoSum(_ nums: , _ target: Int) ->  {
    var dictionary = ()
   for (i, n) in nums.enumerated() {
       if let last = dictionary {
           return 
       }
       dictionary = i
   }
   return 
}</code></pre>
<!-- /wp:code -->