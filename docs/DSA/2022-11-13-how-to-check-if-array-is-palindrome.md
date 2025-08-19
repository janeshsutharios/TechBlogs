---
title: "How to check if array is Palindrome ?"
date: 2022-11-13 06:02:24
categories: ['Array-Strings', 'check if array is palindrome swift', 'DSA']
layout: post
---

<!-- wp:paragraph -->
 Check weather array is palindrome Example :  ===> It's palindrome<br> Solution#: Here we are checking first & last element equality & increase till mid of array


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// Question# : Check Palindrome of array.
func checkPalindrome(inArray: inout , startIndex: inout Int) ->Bool {
    if startIndex >= inArray.count/2 {return true}
    if inArray != inArray { return false}
    startIndex += 1
    return checkPalindrome(inArray: &inArray, startIndex: &startIndex)
}
var inArray3 = 
var startIndex3 = 0
print(checkPalindrome(inArray: &inArray3, startIndex: &startIndex3))</code></pre>
<!-- /wp:code -->