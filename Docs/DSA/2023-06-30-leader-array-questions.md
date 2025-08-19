---
title: "Leader array questions."
date: 2023-06-30 12:38:16
categories: ['Array-Strings']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/replace-elements-with-greatest-element-on-right-side/description/" target="_blank" rel="noopener" title=""> </a>.Given an array <code>arr</code>, replace every element in that array with the greatest element among the elements to its right, and replace the last element with <code>-1</code>


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">Example 1::
<strong>Input:</strong> arr = 
<strong>Output:</strong> 
<strong>Explanation:</strong> 
- index 0 --> the greatest element to the right of index 0 is index 1 (18).
- index 1 --> the greatest element to the right of index 1 is index 4 (6).
- index 2 --> the greatest element to the right of index 2 is index 4 (6).
- index 3 --> the greatest element to the right of index 3 is index 4 (6).
- index 4 --> the greatest element to the right of index 4 is index 5 (1).
- index 5 --> there are no elements to the right of index 5, so we put -1.</pre>
<!-- /wp:preformatted -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: O(N)
// SC: O(N)
func replaceElements(_ arr: ) ->  {
    let arrayCount = arr.count
    if arrayCount == 0 {return }
    let lastIndex = arrayCount - 1
    var nums = Array.init(repeating: -1, count: arrayCount)
    var curMax = arr
    
    nums = -1// As per question requirement
    
    for i in stride(from: lastIndex - 1, through: 0, by: -1) {
        let temp = curMax
        curMax = max(curMax, arr)
        nums = temp
    }
    return nums
}

var leaderArr1 = 
let leaderArrayOutput1 = replaceElements(leaderArr1)
print("leaderArrayOutput1 array-->", leaderArrayOutput1) </code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
<a href="https://takeuforward.org/data-structure/leaders-in-an-array/" target="_blank" rel="noopener" title=""> : </a><strong>Problem Statement:</strong> Given an array, print all the elements which are leaders. A Leader is an element that is greater than all of the elements on its right side in the array


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Example 1:</strong>
<strong>Input:</strong>
 arr = 
<strong>Output</strong>:
 7 1 0
<strong>Explanation:</strong>
 Rightmost element is always a leader. 7 and 1 are greater than the elements in their right side.</pre>
<!-- /wp:preformatted -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC O(N)
// SC O(N)
func findLeader(arr: ) -> {
    var leader = arr.last ?? 0
    var leaderArray: = //  Last will always leader because no elements are on right
    for obj in stride(from: arr.count-2, to: 0, by: -1) {
        if arr > leader {// If element is greater than leader append it into new array
            leader = arr
            leaderArray.append(leader)
        }
    }
    return leaderArray
}

var leaderArr = 
let leaderArrayOutput = findLeader(arr: leaderArr)
print("Leader array-->", leaderArrayOutput)//</code></pre>
<!-- /wp:code -->