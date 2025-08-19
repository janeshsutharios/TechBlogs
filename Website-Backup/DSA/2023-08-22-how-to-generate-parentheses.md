---
title: "How to generate parentheses"
date: 2023-08-22 04:23:24
categories: ['Recursion']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/generate-parentheses/" target="_blank" rel="noopener" title="">: </a>Given <code>n</code> pairs of parentheses, write a function to <em>generate all combinations of well-formed parentheses</em>.<br>Example: - n = 2.<strong> ---   </strong>


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
Approach: We can solve using backtracking / recursion 


<!-- /wp:paragraph -->

<!-- wp:image {"id":2145,"width":1078,"height":982,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large is-resized">![](/TechBlogs/Assets/Website/2023/08/Generate-paranthesis-recursion-backtracking-1024x933.jpg)</figure>
<!-- /wp:image -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func backtrack(_ current: String,_ open: Int,_ end: Int,_ max: Int, _ result: inout ) {
    if current.count == max * 2 {// Because if n = 2; max parenthesis count is (()) which is n X 2
        result.append(current)
        print("Brackets match ------ ", current)
        return
    }
    
    if open < max {// Example: (( < 2 -- False So don't add open braces
        print("open < max -- Open Bracket-- ", open+1, end, current + "(")
        backtrack(current + "(", open + 1, end, max, &result)
    }
    print("   ")
    if end < open {
        print("end < open -- Open Bracket-- ", open+1, end, current + ")")
        backtrack(current + ")", open, end + 1, max, &result)
    }
}

let generateParath = generateParenthesis(2)
print("parathesis---  ", generateParath)// Ip::1 -> () Ip::2->()() (()) Ip::3-> ((()))", "(()())", "(())()", "()(())", "()()()
</code></pre>
<!-- /wp:code -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">Logs -- 
open < max -- Open Bracket--  1 0 (
open < max -- Open Bracket--  2 0 ((
   
end < open -- Open Bracket--  3 0 (()
   
end < open -- Open Bracket--  3 1 (())
Brackets match ------  (())
   
end < open -- Open Bracket--  2 0 ()
open < max -- Open Bracket--  2 1 ()(
   
end < open -- Open Bracket--  3 1 ()()
Brackets match ------  ()()
parentheses---    // Final output</code></pre>
<!-- /wp:code -->