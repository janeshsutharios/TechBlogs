---
title: "Print one sequence whose sum is K"
date: 2022-11-22 10:55:34
categories: ['DSA', 'printing subsequences whose sum is k', 'Recursion']
layout: post
---

<!-- wp:paragraph -->
 : Print any one sequence whose some is equal to K<br>For example:-  Target Sum = 8 So Output will be  


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func printOneSeqSumK(ind: Int,
                     op: inout ,
                     targetSum: Int,
                     currSum: inout Int,
                     inArray: ,
                     length: Int) -> Bool {
    if ind == length {
        if  targetSum == currSum {
            print("foundTheSum-->", op)
            return true
        }
        return false
    }

    op.append(inArray)
    currSum += inArray

    if printOneSeqSumK(ind: ind+1,
                    op: &op,
                    targetSum: targetSum,
                    currSum: &currSum,
                    inArray: inArray,
                       length: length) { return true}
    op.removeLast()
    currSum -= inArray
    if printOneSeqSumK(ind: ind+1,
                    op: &op,
                    targetSum: targetSum,
                    currSum: &currSum,
                    inArray: inArray,
                       length: length) { return true }
    return false
}


let arrayInput = 
let length = arrayInput.count
var op:  = 
let ind = 0
let targetSum = 8
var currSum = 0
printOneSeqSumK(ind: ind,
                op: &op,
                targetSum: targetSum,
                currSum: &currSum,
                inArray: arrayInput,
                length: length)</code></pre>
<!-- /wp:code -->