---
title: "String to Integer conversion (atoi)"
date: 2023-07-17 09:25:49
categories: ['String']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/string-to-integer-atoi/description/" target="_blank" rel="noopener" title=""></a>: Convert given string into Integer with given condition


<!-- /wp:paragraph -->

<!-- wp:list {"ordered":true} -->
<ol><!-- wp:list-item -->
<li>Discards all leading whitespaces</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>Maintain Sign</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li> ab123a  -> 0</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>-+123  -> 0</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>+-123  -> 0</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li> 123abc-  -> 123</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li> -99999999999999999  -> -2147483648</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li> 00999999999999999  -> 2147483647</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li> 2147483648  -> 2147483647</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li> -2147483648 -> -2147483648</li>
<!-- /wp:list-item --></ol>
<!-- /wp:list -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: O(N)
// SC: O(1)
func myAtoi(_ s: String) -> Int {
    var result = 0// Outpuut
    var sign = 1 // 1 means positive -1 means negative(further multiply)
    var isStarted = false // To skip invalid character.
    for char in s {
        if char == " " {
            if isStarted {
                break
            }
        } else if (char == "-" || char == "+") {
            if isStarted {
                break
            }
            isStarted = true
            if char == "-" {
                sign = -1
            }
        } else if char >= "0" && char <= "9" {
            isStarted = true
            if let val = char.wholeNumberValue {
                result = result*10+val
            }
            if result > Int32.max {
                return sign == 1 ? Int(Int32.max) : Int(Int32.min)
            }
        } else {
            break
        }
    }
    return result*sign
}

let atoiString = "  43   "//"        42       "// "   -42"//"4193 with words"
let atoiOutput = myAtoi(atoiString)
print("output is--  ", atoiOutput)// 43</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":5} -->
<h5 class="wp-block-heading">Approach #2 Using Recursion</h5>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func myAtoiUsingRecursion(_ s: String) -> Int {
    var output = 0
    var startIndex = 0
    var sign:Int = 1
    var isStarted = false
    return myAtoiRec(s, &startIndex, &output, s.count, &sign, &isStarted)
}
func myAtoiRec(_ s: String,
               _ strIndex: inout Int,
               _ result: inout Int,
               _ strCount: Int,
               _ sign: inout Int,
               _ isStarted: inout Bool) -> Int {
    
    if strIndex == strCount { return result*sign }
    let curChar = s
    if curChar == " " {
        if isStarted { return result*sign }
    } else if (curChar == "-" || curChar == "+") {
        if isStarted { return result*sign }
        isStarted = true
        if curChar == "-" {
            sign = -1
        }
    } else if curChar >= "0" && curChar <= "9" {
        isStarted = true
        if let val = curChar.wholeNumberValue {
            result = result*10+val
        }
        if result > Int32.max {
            return sign == 1 ? Int(Int32.max) : Int(Int32.min)
        }
    } else {
        return result*sign
    }
    strIndex+=1
    return myAtoiRec(s, &strIndex, &result, strCount, &sign, &isStarted)
}</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":4} -->
<h4 class="wp-block-heading">Plain Atoi Solution</h4>
<!-- /wp:heading -->

<!-- wp:code {"lineNumbers":true} -->
<pre class="wp-block-code"><code lang="swift" class="language-swift line-numbers">// Plain AsciiToInterger function..
func myAtoiRec(_ s: String,_ strIndex: inout Int, _ result: inout Int, _ strCount: Int) -> Int {
    if strIndex == strCount { return result }
    if let val = s.wholeNumberValue {
        result = result*10+val
        strIndex+=1
    }
    return myAtoiRec(s, &strIndex, &result, strCount)
}</code></pre>
<!-- /wp:code -->