---
title: "Maximum Nesting Depth of the Parentheses"
date: 2023-07-17 05:09:52
categories: ['String']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/maximum-nesting-depth-of-the-parentheses/description/" target="_blank" rel="noopener" title="">: </a>In a given string find maximum depth of parentheses. input string has only "( )" type parentheses<br>Example: Input =  "(1+(5*8)+((9)/2))+100"  ||  Output = 2 


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: O(N)
// SC: O(1)
func maxDepth(_ s: String) -> Int {
    var res = 0;
    var cur = 0
    
    for c in s {
        if c == "(" {
            cur += 1
            res = max(res, cur)
        }
        if c == ")" {
            cur -= 1
        }
    }
    return res
}
let ipParanth = "(1+(5*8)+((9)/2))+100"
let opMaxDepth = maxDepth(ipParanth)
print("max depth--", opMaxDepth)// 3</code></pre>
<!-- /wp:code -->