---
title: "How to find max consecutive 1's with Kth allowed zero flip ?"
date: 2023-02-11 09:43:23
categories: ['Array-Strings', 'Max Consecutive Ones III', 'sliding window algorithm', 'sliding window technique']
layout: post
---

<!-- wp:paragraph -->
 In a. Given a binary array <code>nums</code> and an integer <code>k</code>, find <em>the maximum number of consecutive </em><code>1</code><em>'s in the array & you can flip at most</em>  <code>k</code> <code>0</code>'s.<br>Example: - var arrMix =  <br>var arrCount = 11 <br>var maxZeros = 2<br>Hence the output will be 8  i.e <mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">1, 1, 0, 1, 0, 1, 1, 1</mark><br>This Question can solve by simple sliding window approach <br>In the below code  I have declared <code>startWindowIndex</code> & <code>endWindowIndex</code> we starts moving with loop and if we find zero element we increments <code>maxZeros</code> & at certain time if <code>maxZeros</code> became negative we increase <code>startWindowIndex</code> and as we already decremented <code>maxZeros</code> so now we will allow to enter more zeros if any by  <code>maxZeros += 1</code>


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: O(n)
// SC: O(1)
func maxConsecutiveOfonesWithFlipiingZeros(arr: inout ,
                                           arrCount: inout Int,
                                           maxZeros: inout Int) -> Int {
    
    var startWindowIndex = 0
    var endWindowIndex = 0
    
    for currentWindowIndex in 0..<arrCount {
        if arr == 0 {
            maxZeros -= 1
        }
        if maxZeros<0 {
            startWindowIndex += 1
            if arr == 0 {
                maxZeros += 1
            }
        }
        endWindowIndex = currentWindowIndex
    }
    return endWindowIndex-startWindowIndex// returns the desired window.
}

var arrMix = 
var arrCount = 11
var maxZeros = 2
let op = maxConsecutiveOfonesWithFlipiingZeros(arr: &arrMix,
                                               arrCount: &arrCount,
                                               maxZeros: &maxZeros)
print("op", op)// Prints 8</code></pre>
<!-- /wp:code -->