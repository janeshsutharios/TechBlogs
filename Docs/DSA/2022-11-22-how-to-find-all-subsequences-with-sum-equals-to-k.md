---
title: "How to Find all subsequences with sum equals to K"
date: 2022-11-22 10:40:49
categories: ['DSA', 'find all subsequences with sum equal to k swift', 'Recursion']
layout: post
---

<!-- wp:paragraph -->
 : In a given array find all possible sequence whose sum is certain number:<br> For example:-   Target Sum = 8 So Output will be  


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func printAllSeqSumK(ind: Int,
                     op: inout ,
                     targetSum: Int,
                     currSum: inout Int,
                     inArray: ,
                     length: Int) {
    if ind == length {
        if  targetSum == currSum {
            print("foundTheSum-->", op)
        }
        return
    }
        
    op.append(inArray)
    currSum += inArray
  
    printAllSeqSumK(ind: ind+1,
                    op: &op,
                    targetSum: targetSum,
                    currSum: &currSum,
                    inArray: inArray,
                    length: length)
    op.removeLast()
    currSum -= inArray

    printAllSeqSumK(ind: ind+1,
                    op: &op,
                    targetSum: targetSum,
                    currSum: &currSum,
                    inArray: inArray,
                    length: length)
}


let arrayInput = 
let length = arrayInput.count
var op:  = 
let ind = 0
let targetSum = 8
var currSum = 0
printAllSeqSumK(ind: ind,
                op: &op,
                targetSum: targetSum,
                currSum: &currSum,
                inArray: arrayInput,
                length: length)</code></pre>
<!-- /wp:code -->