---
title: "Reverse words in String"
date: 2023-07-15 12:15:02
categories: ['String']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/reverse-words-in-a-string/description/" target="_blank" rel="noopener" title=""></a> Given a string s, reverse the words of the string.<br>Note: Remove extra spaces from output


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<strong>Examples:</strong>


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Example 1:</strong>
<strong>Input:</strong> s=”My Name is Janesh”
<strong>Output:</strong> “Janesh is Name My”

<strong>Example 2:</strong>
<strong>Input:</strong> s= "  My     Name    is Janesh"
<strong>Output:</strong> "Janesh is Name My"</pre>
<!-- /wp:preformatted -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: O(N)
// SC: O(1)
func reverseWords(_ s: String)-> String {
    var left = 0
    let right = s.count - 1
    var temp = ""
    var ans = ""
    
    // Iterate the string and keep on adding to form a word to temp & transfer to ans
    // If empty space is encountered then add the current word to the ans
    while left <= right {
        let indexEl = s.index(s.startIndex, offsetBy: left)
        var ch = String(s)
        if ch != " " {
            temp += ch// fill word into temp
        } else if ch == " " {// move data from temp to answer & reset temp
            if ans != "" {
                if temp != "" {// If contiguous element is " " empty string don't add any more white space
                    ans = temp + " " + ans
                }
            } else {
                ans = temp
            }
            temp = ""
        }
        left+=1
    }
    
    //If temp is not empty string then add to the result(Last word to be added)
    if temp != "" {
        if ans != "" {
            ans = temp + " " + ans
        } else {
            ans = temp
        }
    }
    
    return ans
}

let stringToReverseWords = "  My     Name    is Janesh"
let opWords =  reverseWords(stringToReverseWords)
print("op words--->", opWords, opWords.count)//op words---> Janesh is Name My 17</code></pre>
<!-- /wp:code -->