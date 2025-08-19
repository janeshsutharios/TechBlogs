---
title: "How to check Isomorphic Strings?"
date: 2023-07-16 12:27:15
categories: ['String']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/isomorphic-strings/description/" target="_blank" rel="noopener" title="">:</a> Given two strings <code>s</code> and <code>t</code>, <em>determine if they are isomorphic</em>.


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<strong>Definition</strong>: Two strings <code>s</code> and <code>t</code> are isomorphic if the characters in <code>s</code> can be replaced to get <code>t</code>.


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character, but a character may map to itself.


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<strong>Example 1:</strong>


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Input:</strong> s = "egg", t = "add"
<strong>Output:</strong> true</pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<strong>Example 2:</strong>


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Input:</strong> s = "foo", t = "bar"
<strong>Output:</strong> false</pre>
<!-- /wp:preformatted -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: O(N)
// SC: O(N)
func isIsomorphic(_ s: String, _ t: String) -> Bool {
    var rightDic = (), leftDic = rightDic
    for i in s.indices {
        guard rightDic] == leftDic] else { return false }
        rightDic] = i
        leftDic] = i
    }
    return true
}

let iso1 = "egg"
let iso2 = "add"
let isISO = isIsomorphic(iso1, iso2)
print("isISO--- ", isISO) // true</code></pre>
<!-- /wp:code -->