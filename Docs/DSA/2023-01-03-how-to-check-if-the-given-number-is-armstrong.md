---
title: "How to check if the given number is Armstrong ?"
date: 2023-01-03 07:29:05
categories: ['armstrong number formula', 'armstrong number in swift', 'Array-Strings']
layout: post
---

<!-- wp:paragraph -->
<a href="https://www.geeksforgeeks.org/program-for-armstrong-numbers/" target="_blank" rel="noopener" title="">: </a>Check if given number is Armstrong. for example :<strong> <mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">371 =  3 pow 3 + 7 <strong><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">pow</mark></strong> 3 + 1 <strong><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">pow</mark> </strong>3 = 371</mark></strong>  The count of digits to power of each digits & sum is equivalent to self number.<a href="https://developer.apple.com/documentation/foundation/1779833-pow" target="_blank" rel="noopener" title=""> (pow id power )</a>


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func checkArmStrong(n: inout Int) -> Bool {
    var count = 0
    var firstCopy = n
    var originalCopy = n
    var sumOfPower = 0
    
    while firstCopy != 0 {
        count+=1
        firstCopy = firstCopy/10
    }
    
    while n != 0 {
        let digit = n%10
        sumOfPower += Int(pow(Double(digit), Double(count)))
        n = n/10
    }
    return sumOfPower == originalCopy
    
}

var ipNumber = 153
print(checkArmStrong(n: &ipNumber))// true.</code></pre>
<!-- /wp:code -->