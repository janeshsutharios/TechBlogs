---
title: "How to find Longest Common Prefix in strings Array"
date: 2023-07-17 03:40:38
categories: ['String']
layout: post
---

<!-- wp:paragraph -->
: In a given string array find the longest common prefix <br>Example: Input <br>Output: "fl"// because this is common prefix in the given string.


<!-- /wp:paragraph -->

<!-- wp:heading {"level":5} -->
<h5 class="wp-block-heading">#Approach Binary search</h5>
<!-- /wp:heading -->

<!-- wp:paragraph -->
We will create two pointers low & high, low starts from 0 & high is first object count. so now we will divide string into two parts and compare substring with all the object if it's matched with remaning  strings means there is more chances we can get hence we increment lower counter to mid+1. Now if all string not satisfy with prefixes then move higher pointer to mid because till mid we are good.


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// Approach Binary search
// TC: O(nlog(n))
// SC: O(1)
func longestCommonPrefix(_ strs: ) -> String {
    guard let firstStr = strs.first else { return "" }
    
    var low = 0
    var high = firstStr.count
    
    while low < high {// Divide first array object into two parts & compare
        let mid = (low + high) / 2
        let prefix = String(firstStr.prefix(mid + 1))
        
        if strs.allSatisfy({ $0.hasPrefix(prefix) }) {// if mid is satisfy increment counter of low
            low = mid + 1
        } else {// if larger string doesn't match decrement high
            high = mid
        }
    }
    
    return String(firstStr.prefix(low))
}
let commonPrefixStr = 
let opCommonStr = longestCommonPrefix(commonPrefixStr)
print("opCommonStr-- ", opCommonStr)// "fl"</code></pre>
<!-- /wp:code -->