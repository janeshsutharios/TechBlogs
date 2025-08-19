---
title: "Count frequency of each element in an array"
date: 2023-01-04 06:26:01
categories: ['Array-Strings', 'Find the number of occurrences of a given digit in a number']
layout: post
---

<!-- wp:paragraph -->
: Count frequency of each element in a given array .<br>For example: Given Array . Output is <strong></strong> Which indicates 4 is 1 time, 6 is 2 times and so on...<br>#Approach 1: - Use HashMap /Dictionary . Because dictionary key are unique so we can use of that & keep values as counter  


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: O(n)
// SC: O(n)
func findOccurance(_ arr: ) ->  {
    
    var hashObject:  = 
    for obj in arr {
        if hashObject == nil {
            hashObject = 1
        } else {
            hashObject! += 1
        }
    }
    return hashObject
}

var anArray = 
let hashObj = findOccurance(anArray)
print("Hash obj---", hashObj) // </code></pre>
<!-- /wp:code -->