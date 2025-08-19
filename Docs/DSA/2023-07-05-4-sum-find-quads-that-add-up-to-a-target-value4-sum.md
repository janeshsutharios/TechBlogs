---
title: "4 Sum | Find Quads that add up to a target value4 Sum"
date: 2023-07-05 07:14:18
categories: ['Array-Strings']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/4sum/description/" target="_blank" rel="noopener" title="">:</a> Find Quads that add up to a target value4 Sum


<!-- /wp:paragraph -->

<!-- wp:heading {"level":5} -->
<h5 class="wp-block-heading">Approach# using the 4 pointers</h5>
<!-- /wp:heading -->

<!-- wp:paragraph -->
Two pointers a & b are fixed and we have two moving pointers c and d. where c starts from b + 1 and d is start from last index


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">
func fourSum(_ nums: , _ target: Int) -> ] {
    let len = nums.count
    guard len >= 4 else { return  }// minimum 4 items required for 4 sum
    
    var result = ]()
    let sort = nums.sorted()
    
    for a in 0..<(len - 1) where a == 0 || sort != sort { // if sort == sort discard the loop // a is fix pointer
        for b in (a + 1)..<len where b == a + 1 || sort != sort {// if sort == sort discard the loop // b is fix pointer
            var c = b + 1, d = len - 1// c pointer is b+1 which is movable
            while c < d {// As array is sorted check if c pointer doesn't jump
                let val = (a: sort, b: sort, c: sort, d: sort)
                let sum = (val.a + val.b + val.c + val.d)
                if sum == target { result.append() }// add result to the array as we found the desired sum
                if sum < target {
                    while sort == val.c, c < d { c += 1 }// increment c pointer as we get lesser sum
                } else {
                    while sort == val.d, d > b { d -= 1 }// decrement d pointer which is the last
                }
            }
        }
    }
    return result
}

let fourSumInputArray = 
let fourSumOutputArray = fourSum(fourSumInputArray, 0)
print("Output array-->", fourSumOutputArray) //, , ]
</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":5} -->
<h5 class="wp-block-heading">Complexity Analysis</h5>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<strong>Time Complexity: </strong>O(N<sup>3</sup>), where N = size of the array.<br><strong>Reason: </strong>Each of the pointers c and d, is running for approximately N times. And both the pointers k and l combined can run for approximately N times including the operation of skipping duplicates. So the total time complexity will be O(N<sup>3</sup>). 


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<strong>Space Complexity: </strong> O(n) where we stores the result.


<!-- /wp:paragraph -->