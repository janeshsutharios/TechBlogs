---
title: "How to create Pascal's Triangle in swift"
date: 2022-11-01 11:31:57
categories: ['Array-Strings', 'DSA', 'Pascal triangle', 'Swift Algorithm', 'Swift DSA']
layout: post
---

<!-- wp:paragraph -->
 In <strong>Pascal's triangle</strong>, each element is the sum of the two numbers directly above it. 


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func generate(_ numRows: Int) -> ] {
    var pascalObject = ](repeating: (), count: numRows)
    
    for firstElement in 0..<numRows {
        pascalObject = (repeating: 0, count: firstElement+1)
        
        for secondElement in 0..<firstElement+1 {
            if secondElement == 0 || secondElement == firstElement {
                pascalObject = 1
            } else {
                let addition = pascalObject + pascalObject
                pascalObject = addition
            }
        }
    }
    
    return pascalObject
}</code></pre>
<!-- /wp:code -->