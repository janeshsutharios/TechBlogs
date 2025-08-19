---
title: "Check if two strings are anagrams"
date: 2023-07-16 10:59:34
categories: ['String']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/valid-anagram/description/" target="_blank" rel="noopener" title="">:</a> Given two string check weather they anagram<br>Example: abc & cab are anagram


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: O(N)
// SC: O(N)
func isAnagram(_ s: String, _ t: String) -> Bool {
    var arr = (repeating: 0, count: 26)
    for char in s {
        arr += 1// Modulo is used to use values from 0 to 25 which is array optimised size.
    }
    for char in t {
        arr -= 1

    }
    for v in arr where v != 0  {
        return false// If some value are non zero means different objects
    }
    return true
 // Or we can also use contains   return !arr.contains(where: { $0 != 0 })
}

let ana1 = "abc"
let ana2 = "cab"
let isAna = isAnagram(ana1, ana2)
print("isAna--- ", isAna) // true</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":5} -->
<h5 class="wp-block-heading">Approach #2 Using Hash map / Dictionary </h5>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: O(N)
// SC: O(N)
func isAnagram2(_ s: String, _ t: String) -> Bool {
    guard s.count == t.count else { return false }
    
    var map = ()
    for char in s {
        map += 1// filling first String characters count into map
    }
    
    for char in t {
        map -= 1// removing second String characters count from map. Means all values in map should zero
    }
    for v in map.values where v != 0  {
        return false// If some value are non zero means different objects
    }
    return true
   // return map.values.filter { $0 > 0 }.count == 0
}</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":5} -->
<h5 class="wp-block-heading">Approach #3:  Using reduce function.</h5>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: O(N).. because by default swift reduce function uses O(N) based on input
func isAnagram3(_ s: String, _ t: String) -> Bool {
    return getCharacterMap(s) == getCharacterMap(t)
}

func getCharacterMap(_ s: String) ->  {
    return s.reduce(into: , { $0 += 1 })
}</code></pre>
<!-- /wp:code -->