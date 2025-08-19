---
title: "How to find duplicates in Array?"
date: 2022-11-12 03:03:17
categories: ['Array-Strings', 'DSA', 'Find array duplicates in swift']
layout: post
---

<!-- wp:paragraph -->
 In a given array return true if array have duplicate elements . For example 1  : = True  example 1  : = False  


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">class Solution {
    // Time Complexity o(n)
    // Space Complexity o(1) 
    func containsDuplicate(_ nums: ) -> Bool {
        var dict:  = 
        for value in nums {
            if dict == nil {
                dict = 0
            } else {
                return true
            }
        }
        return false
    }
}</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
So here we have used Dictionary which is Hashable which contains only unique keys hence we can find duplicates elements in swift.


<!-- /wp:paragraph -->