---
title: "Find all elements that appear more than ⌊ n/3 ⌋ times."
date: 2023-07-04 15:03:56
categories: ['Array-Strings']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/majority-element-ii/description/" target="_blank" rel="noopener" title="">: </a>Given an integer array of size <code>n</code>, find all elements that appear more than <code>⌊ n/3 ⌋</code> times.<br>Example: Input =  ; Output:--// 


<!-- /wp:paragraph -->

<!-- wp:heading {"level":6,"textColor":"ast-global-color-2"} -->
<h6 class="wp-block-heading has-ast-global-color-2-color has-text-color">Approach:  By using dictionary</h6>
<!-- /wp:heading -->

<!-- wp:list -->
<ul><!-- wp:list-item -->
<li>Create an empty dictionary and assign the numbers count</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>Create another loop and filter elements which are greater than the n/3</li>
<!-- /wp:list-item --></ul>
<!-- /wp:list -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: O(2N)
// SC: O(2N)
func majorityElementNBy3(_ nums: ) ->  {
    if nums.isEmpty { return  }
    var frequencyDictionary: Dictionary<Int,Int> = , result:  = 
    for num in nums {
        frequencyDictionary += 1
    }
    for (key,val) in frequencyDictionary where val > (nums.count/3) {
        result.append(key)
    }
    return result
}

let majority3Input = ;
let majority3Output = majorityElementNBy3(majority3Input);
// print("The majority elements are: ", majority3Output); // 11, 33</code></pre>
<!-- /wp:code -->