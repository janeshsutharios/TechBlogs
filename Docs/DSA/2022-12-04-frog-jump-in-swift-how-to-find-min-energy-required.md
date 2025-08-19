---
title: "Frog jump in swift || How to find min energy required ?"
date: 2022-12-04 16:39:18
categories: ['DSA', 'Dynamic programming in swift', 'DynamicProgramming', 'frog jump in swift']
layout: post
---

<!-- wp:paragraph -->
<a href="https://www.codingninjas.com/codestudio/problems/frog-jump_3621012" target="_blank" rel="noopener" title=""> </a>Find minimum total energy used by frog to reach from 1st stair to nth stair. He can jump from i+1 or i+2 stair.


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// Approach 1: Using dynamic programming & recursion 
// Time complexity O(n)
// Space Complexity O(n)
func frogJump(_ n : Int, _ height: , dp: inout ) -> Int {
       dp = 0
    for i in 1..<n {
        var fs = dp + abs(height - height)
        var ss = Int.max
        if i > 1 {
            ss = dp + abs(height - height)
        }
        dp = min(fs, ss)

    }
    return dp
}

var n = 6
var heights:  = 
var dp:  = Array.init(repeating: -1, count: n+1)
let resultValue = frogJump(n, heights, dp: &dp)
print(resultValue)// output 40

// Approach 2: Using Tabulation (bottom up) Optimum space.
// Time complexity O(n)
// Space Complexity O(1)
func frogJump(_ n : Int, _ height: ) -> Int {
    var prev1 = 0
    var prev2 = 0
    for i in 1..<n {
        var fs = prev1 + abs(height - height)
        var ss = Int.max
        if i > 1 {
            ss = prev2 + abs(height - height)
        }
        var curr = min(fs, ss)
        prev2 = prev1
        prev1 = curr
        
    }
    return prev1
}
var n = 6
var heights:  = 
let resultValue = frogJump(n, heights)
print(resultValue) // output 40
</code></pre>
<!-- /wp:code -->