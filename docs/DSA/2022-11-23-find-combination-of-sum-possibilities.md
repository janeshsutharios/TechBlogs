---
title: "Find combination of sum possibilities"
date: 2022-11-23 11:23:30
categories: ['DSA', 'Recursion', 'sum of array combinations']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/combination-sum/" target="_blank" rel="noopener" title="">: </a> In a distinct array a target integer <code>target</code>, return <em>a list of all <strong>unique combinations</strong> of </em> <code>candidate</code><br><strong>Input:</strong> candidates = , target = 7 <strong>Output:</strong> ,]


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func seqCombinationWithSumK(ind: Int,
                            target: Int,
                            op: inout ,
                            inArray: ,
                            length: Int,
                            ans: inout ]) {
    if ind == length {
        if target == 0 {
            ans.append(op)
        }
        return
    }
    // Pick An Element
    if (inArray <= target) {
        op.append(inArray)
        seqCombinationWithSumK(ind: ind,
                               target:target - inArray,
                               op: &op,
                               inArray: inArray,
                               length: length,
                               ans: &ans)
        op.removeLast()
    }
    // Not Pick condition.
    seqCombinationWithSumK(ind: ind+1,
                           target:target,
                           op: &op,
                           inArray: inArray,
                           length: length,
                           ans: &ans)
}


let inArray = 
let length = inArray.count
var op:  = 
var ans: ] = 
let currentIndex = 0
let target = 7
seqCombinationWithSumK(ind: currentIndex,
                       target: target,
                       op: &op,
                       inArray: inArray,
                       length: length,
                       ans: &ans)

print("answer,", ans)</code></pre>
<!-- /wp:code -->