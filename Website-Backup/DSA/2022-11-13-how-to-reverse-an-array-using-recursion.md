---
title: "How to reverse an array using recursion ?"
date: 2022-11-13 04:56:01
categories: ['DSA', 'how to reverse an array using recursion in swift', 'Recursion']
layout: post
---

<!-- wp:heading {"level":6,"textColor":"ast-global-color-1"} -->
<h6 class="has-ast-global-color-1-color has-text-color"> : Reverse array using recursion Example:  = .  Approach #1 using two variables : - </h6>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// Question reverse the string using recursion
// Here we are just swapping right with left & increase the left & right elements
func reverseArrayUsingRecursion(inArray: inout ,
                   rightElement: inout Int,
                   leftElement: inout Int) {
    
    if rightElement >= leftElement {return}
    inArray.swapAt(rightElement, leftElement)
    rightElement += 1
    leftElement -= 1
    reverseArrayUsingRecursion(inArray: &inArray,
                  rightElement: &rightElement,
                  leftElement: &leftElement)
}

var inArray = 
var rightElement = 0
var leftElement = inArray.count - 1
reverseArrayUsingRecursion(inArray: &inArray, rightElement: &rightElement, leftElement: &leftElement)
print(inArray) // prints </code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":6,"textColor":"ast-global-color-1"} -->
<h6 class="has-ast-global-color-1-color has-text-color"><strong>// Approach#2: Using single pointer/variable so we written base case which blocks on n/2, we are just increasing the element by +1 on every recursion till half of the array.</strong></h6>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func reverseArrayUsingRecursion2(inArray: inout ,
                                 startIndex: inout Int) {
    
    if startIndex >= inArray.count/2 {return}
    inArray.swapAt(startIndex, inArray.count-startIndex-1)
    startIndex += 1
    reverseArrayUsingRecursion2(inArray: &inArray,
                                startIndex: &startIndex)
}

var inArray2 = 
var startIndex = 0
reverseArrayUsingRecursion2(inArray: &inArray2, startIndex: &startIndex)
print(inArray2)</code></pre>
<!-- /wp:code -->