---
title: "How to find sum of first N numbers in swift ?"
date: 2022-11-12 17:25:39
categories: ['Array-Strings', 'DSA', 'find sum of first N numbers in swift']
layout: post
---

<!-- wp:heading {"level":6,"textColor":"ast-global-color-1"} -->
<h6 class="has-ast-global-color-1-color has-text-color"># Question 1:  Find sum of first n numbers. Example :-- n = 3 => 3+2+1 =6. We will use recursion to solve this problem.</h6>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func sumOfNNumber(number: Int, sum: inout Int) -> Int{
    if number < 1 {
        return sum
    }
    sum += number
    sumOfNNumber(number: number - 1, sum: &sum)
    return sum
}
var sumValue = 0
sumOfNNumber(number: 3, sum: &sumValue)
print(sumValue)

// Approach 2 sun of first n mumbers

func sumOfFirstNNumer(number: Int) -> Int {
    if number == 0 { return 0 }
    return number + sumOfFirstNNumer(number: number - 1)
}
print(sumOfFirstNNumer(number: 4))</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":6,"textColor":"ast-global-color-1"} -->
<h6 class="has-ast-global-color-1-color has-text-color"># Question 2: Find sum of array elements using recursion approach : </h6>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func sumOfArray(inArray: , arrayCount: inout Int, sum: inout Int)  {
    if arrayCount <= 0 {
        return
    }
    arrayCount -= 1
    sum += inArray
    sumOfArray(inArray: inArray, arrayCount: &arrayCount, sum: &sum)
}


var arrayInput = 
var arrayCount = arrayInput.count
var sum = 0
sumOfArray(inArray: arrayInput, arrayCount: &arrayCount, sum: &sum)
print(sum)</code></pre>
<!-- /wp:code -->