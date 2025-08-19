---
title: "How to reverse String in swift?"
date: 2022-11-02 06:42:25
categories: ['Array Reverse', 'Array-Strings', 'DSA', 'DSA Swift', 'Swift Algorithm']
layout: post
---

<!-- wp:paragraph -->
: Reverse a string with O(1) extra memory. The input string is given as an array of characters like  


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func makeReverseArray(_ s: inout ) {
    for i in 0..<s.count/2 {
        //s.swapAt(s.count - i - 1, i) // by using Apple's predefined function.
        (s,s)  = (s,s)
    }
}

var charsInput: = 
makeReverseArray(&charsInput)
print("output-->", charsInput) // Prints 
</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
So here we have used one for loop which iterates half of array & swapping last with first


<!-- /wp:paragraph -->