---
title: "Find largest odd Number/Sequence in String"
date: 2023-07-15 14:20:24
categories: ['String']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/largest-odd-number-in-string/description/" target="_blank" rel="noopener" title="">: </a>In integer string Return <em>the <strong>largest-valued odd</strong> integer (as a string) that is a <strong>non-empty substring</strong> of </em><code>num</code><em>, or an empty string </em><code>""</code><em> if no odd integer exists</em>.


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
A <strong>substring</strong> is a contiguous sequence of characters within a string.


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<strong>Example 1:</strong>


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Input:</strong> num = "52"
<strong>Output:</strong> "5"
<strong>Explanation:</strong> The only non-empty substrings are "5", "2", and "52". "5" is the only odd number</pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
input 25 - Op- 25. <br>input 4324 - Op- 43. 


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: O(N)
// SC: O(N)
func largestOddNumber(_ num: String) -> String {
    if num.isEmpty { return "" }
    // #Approach #1: by iterating from last index Time limit exceed for large input
    var last = num.count - 1
    while last >= 0 {
        let currentChar = String(num)
        if Int(currentChar)! % 2 == 0 {
            last -= 1
        } else {// Re
            let range = num.startIndex...num.index(num.startIndex, offsetBy: last)
            return String(num)// return the all numbers from the odd index
        }
    }
    return ""
    
    // Approach #2 using clousers
    //    guard let i = num.lastIndex(where: { Int(String($0))! % 2 == 1 }) else { return "" }
    //      return String(num)
}

let ipStr = "4324"
let opStr = largestOddNumber(ipStr)
print("op is ", opStr)//43</code></pre>
<!-- /wp:code -->