---
title: "Count All Possible Sequence whose sum is K"
date: 2022-11-22 11:04:37
categories: ['check whether a subsequence exists with sum equal to k', 'DSA', 'Recursion']
layout: post
---

<!-- wp:paragraph -->
: In an array count all possible sequence whose sum is K. <br>example:-  Target Sum = 8 So Output will be 2  because sequences are:    


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func printOneSeqSumK(ind: Int,
                     targetSum: Int,
                     currSum: inout Int,
                     inArray: ,
                     length: Int) -> Int {
    if ind == length {
        if  targetSum == currSum {
            return 1
        }
        return 0
    }
    
    currSum += inArray
    let left = printOneSeqSumK(ind: ind+1,
                    targetSum: targetSum,
                    currSum: &currSum,
                    inArray: inArray,
                       length: length)
    currSum -= inArray
    let right = printOneSeqSumK(ind: ind+1,
                    targetSum: targetSum,
                    currSum: &currSum,
                    inArray: inArray,
                       length: length)
    return left + right
}


let arrayInput = 
let length = arrayInput.count
let ind = 0
let targetSum = 8
var currSum = 0
let allPossibleSum = printOneSeqSumK(ind: ind,
                targetSum: targetSum,
                currSum: &currSum,
                inArray: arrayInput,
                length: length)
print(allPossibleSum)</code></pre>
<!-- /wp:code -->

<!-- wp:image {"id":1565,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large">![](/TechBlogs/Assets/Website/2022/11/Count_all_sequence_whose_sumisK-1-1024x497.jpg)</figure>
<!-- /wp:image -->