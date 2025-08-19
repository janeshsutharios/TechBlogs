---
title: "How to check balanced Parenthesis in swift ?"
date: 2022-11-12 13:25:25
categories: ['Check balanced Parenthesis in swift', 'DSA']
layout: post
---

<!-- wp:paragraph -->
: Check if the given string has balanced parenthesis<strong> <code>//Example 1: // //Input: s = "()" //Output: true //Example 2: // //Input: s = "(){}" //Output: true //Example 3: // //Input: s = "(}" //Output: false</code></strong>


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func isValid(_ s: String) -> Bool {
    guard s.count % 2 == 0 else { return false }
    
    var stack:  = 
    //Here we are maintaing stack . adding element with close bracket & removing values from stack if the braces not matched.
    for ch in s {
        switch ch {
        case "(": stack.append(")")
        case "")
        case "{": stack.append("}")
        default:
            // so we are checking the order in which we inserted the bracket if it does not matched with last pop It's unbalanced '
            if stack.isEmpty || stack.removeLast() != ch {
                return false
            }
        }
    }
    
    return stack.isEmpty
}</code></pre>
<!-- /wp:code -->