---
title: "Roman to Int conversion"
date: 2023-07-17 08:43:58
categories: ['String']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/roman-to-integer/description/" target="_blank" rel="noopener" title="">:</a> Convert Roman number into Int, Roman numerals are represented by seven different symbols: <code>I</code>, <code>V</code>, <code>X</code>, <code>L</code>, <code>C</code>, <code>D</code> and <code>M</code>.


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Symbol</strong>       <strong>Value</strong>
I             1
V             5
X             10
L             50
C             100
D             500
M             1000</pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
Example<br> III = 3 <br>IV = 4


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: O(N)
// SC: O(1)
func romanToInt(_ s: String) -> Int {
    var ans = 0, num = 0;
    
    for i in stride(from: s.count - 1, to: -1, by: -1) {
        switch String(s) {
            case "I": num = 1;
            case "V": num = 5;
            case "X": num = 10;
            case "L": num = 50;
            case "C": num = 100;
            case "D": num = 500;
            case "M": num = 1000;
            default: num = 1
        }
        if ans > 4 * num {
            ans -= num
        } else {
            ans += num
        }
    }
    return ans
}

// TC: O(N)
// SC: O(N)
func romanToInt2(_ s: String) -> Int {
      var prev = 0, out = 0
       let dict:  = 

     for i in s {
         let val = dict ?? 0
         let calculation = (val <= prev) ? prev : -prev
         out += calculation
         prev = val
     }
     out += prev
     return out
}

let strRoman = "IV"
let opRoamn = romanToInt(strRoman)
print("roman-- ", opRoamn)// 4</code></pre>
<!-- /wp:code -->