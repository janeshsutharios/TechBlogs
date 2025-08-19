---
title: "How to find longest Substring Without Repeating Characters ?"
date: 2023-07-30 15:39:53
categories: ['Array-Strings']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/longest-substring-without-repeating-characters/description/" target="_blank" rel="noopener" title="">: </a>Given a string <code>s</code>, find the length of the <strong>longest</strong> <strong>substring</strong> without repeating characters.


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<strong>Example 1:</strong>


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Input:</strong> s = "abcabxy"
<strong>Output:</strong> 5
<strong>Explanation:</strong> The answer is "abcxy", with the length of 5</pre>
<!-- /wp:preformatted -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func lengthOfLongestSubstring(_ s: String) -> Int {
    var longest = 0, startIndex = 0
    var charMap:  = 
    for (index, char) in s.enumerated() {
        if let foundIndex = charMap {
            startIndex = max(foundIndex + 1, startIndex)
        }
        longest = max(longest, index - startIndex + 1)
        charMap = index
    }
    return longest
}

let longestSubStrInput = "abcabxy"
let outputOfLongest = lengthOfLongestSubstring(longestSubStrInput)
//print(" output of longest substring without repeating chars", outputOfLongest) // OP->5
</code></pre>
<!-- /wp:code -->

<!-- wp:image {"id":2121,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large">![](/TechBlogs/Assets/Website/2023/07/LongestSubstring_array-1-1024x490.jpg)</figure>
<!-- /wp:image -->