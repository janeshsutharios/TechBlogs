---
title: "Count number of substrings with exactly k distinct characters"
date: 2023-07-18 05:05:43
categories: ['String']
layout: post
---

<!-- wp:paragraph -->
<a href="https://www.geeksforgeeks.org/count-number-of-substrings-with-exactly-k-distinct-characters/" target="_blank" rel="noopener" title="">: </a>You are given a string 'str' of lowercase alphabets and an integer'k' .<br>Your task is to return the count all the possible substrings that have exactly 'k' distinct characters.<br>For example:<br>'str' = abcad and 'k' = 2.<br>We can see that the substrings {ab, bc, ca, ad} are the only substrings with 2 distinct characters. Therefore, the answer will be 4.<br>Example 2: <br>Input ABCDEFGHIJ <br>Output 6


<!-- /wp:paragraph -->

<!-- wp:image {"id":2043,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large">![](/TechBlogs/Assets/Website/2023/07/k-distinct-count-1024x347.jpg)</figure>
<!-- /wp:image -->

<!-- wp:paragraph -->



<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// Question: count with k diffrent charcters.
// TC: O(nXn)
// SC: O(1) Only 26 size array is used, which can be considered constant space.

func most_k_chars(_ s: String, _ k: Int) -> Int {
    if s.isEmpty { return 0 }
    var map: = 
    var num = 0, left = 0
    
    for char in s.indices {
        map, default:0] += 1
        
        while map.count > k {
            let leftIndex = s
            map -= 1
            if map == 0 {
                map = nil
            }
            left+=1
        }
        
        if let i = s.firstIndex(of: s) {
            let indexEl: Int = s.distance(from: s.startIndex, to: i)
            num += indexEl - left + 1
        }
    }
    return num
}

func exact_k_chars(_ s: String, _ k: Int) -> Int {
    return most_k_chars(s, k) - most_k_chars(s, k - 1)
}

var s1 = "abcdefghij"
var k1 = 5
print("Total substrings with exactly ", k1 , " distinct characters : " ,exact_k_chars(s1, k1))// 6
</code></pre>
<!-- /wp:code -->