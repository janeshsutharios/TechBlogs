---
title: "How to Find a number which appears once and other numbers are twice ?"
date: 2023-04-25 08:52:24
categories: ['Array-Strings', 'number-appears-once']
layout: post
---

<!-- wp:paragraph -->
: In a given random array find a number which appears only single time <br><strong>Example : </strong><br>Random array input -   output = 9<br>Solution: <br>Step 1: Create a dictionary. <br>Step 2: Create loop and fill the keys with element occurrence.<br>Step 3: Create a loop and return the dictionary element which has only single occurrence .<br>T C : O(2n)   S C : O(n) 


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// Question : Find the number that appears once, and the other numbers twice
T C : O(2n)   S C : O(n) 
func findNumberAppearOnce(arr: inout ) -> Int {
    // setting up empty dictionary
    var hashObject:  = 
    // Fill the dictionary with elements occurrence count 
    for obj in arr {
        if hashObject == nil {
            hashObject = 1
        } else {
            hashObject!+=1
        }
    }
// Return the dictionary element which has only single occurrence 
    for (key, _) in hashObject where hashObject == 1 {
      return key
    }
    return -1
}

var randomArray:  = 
let uniqueAppearNumber = findNumberAppearOnce(arr: &randomArray)
print(" uniqueAppearNumber ", uniqueAppearNumber)// prints 9</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
Approach 2(Optimum) :-  Using XOR operation <br>XOR operation gives value if 0 & value => value & 1^1 = 0 


<!-- /wp:paragraph -->

<!-- wp:table -->
<figure class="wp-block-table"><table><tbody><tr><td class="has-text-align-center" data-align="center">1</td><td class="has-text-align-center" data-align="center">0</td><td class="has-text-align-center" data-align="center">1</td></tr><tr><td class="has-text-align-center" data-align="center">0</td><td class="has-text-align-center" data-align="center">1</td><td class="has-text-align-center" data-align="center">1</td></tr><tr><td class="has-text-align-center" data-align="center">0</td><td class="has-text-align-center" data-align="center">0</td><td class="has-text-align-center" data-align="center">0</td></tr><tr><td class="has-text-align-center" data-align="center">1</td><td class="has-text-align-center" data-align="center">1</td><td class="has-text-align-center" data-align="center">0</td></tr></tbody></table><figcaption class="wp-element-caption">XOR Table</figcaption></figure>
<!-- /wp:table -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func findNumberAppearOnceUsingXOR(arr: inout ) -> Int {
    var xorOutput = 0
    for obj in arr {
        xorOutput^=obj
    }
    return xorOutput
}</code></pre>
<!-- /wp:code -->