---
title: "Find First and Last Position of Element in Sorted Array"
date: 2023-07-08 13:50:56
categories: ['BinarySearch']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/description/" target="_blank" rel="noopener" title=""> </a>Given an array of integers <code>nums</code> sorted in non-decreasing order, find the starting and ending position of a given <code>target</code> value. If <code>target</code> is not found in the array, return <code></code>.You must write an algorithm with <code>O(log n)</code> runtime complexity.


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<strong>Example 1:</strong>


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<strong>Input:</strong> nums = , target = 8<br><strong>Output:</strong> <br>


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<strong>Example 2:</strong>


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Input:</strong> nums = , target = 6
<strong>Output:</strong> </pre>
<!-- /wp:preformatted -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: O(2log(N))
// SC: O(1)

func findFirstAndLastOccurance(_ arr: , _ targetElement: Int) ->  {
    
    func findFirstOccurance() ->Int {
        let arrayCount = arr.count
        var low = 0
        var high = arrayCount - 1
        var idx = -1
        
        while low <= high {
            let mid = (low + high) / 2
            if arr >= targetElement {
                high = mid - 1;
            } else{
                low = mid + 1;
            }
            if arr == targetElement {
                idx = mid
            }
        }
        return idx
    }
    
    func findLastOccurance() ->Int {
        let arrayCount = arr.count
        var low = 0
        var high = arrayCount - 1
        var idx = -1
        
        while low <= high {
            let mid = (low + high) / 2
            if arr <= targetElement {
                low = mid + 1;
            } else{
                high = mid - 1;
            }
            if arr == targetElement {
                idx = mid
            }
        }
        return idx
    }

    return 
}

var inputBinArray = 
let targetElem = 8
let opFirstAndLast = findFirstAndLastOccurance(inputBinArray, targetElem)
print("opFirstAndLast --- ", opFirstAndLast)// 3, 4</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":5} -->
<h5 class="wp-block-heading">We can also solve a <a href="https://takeuforward.org/data-structure/count-occurrences-in-sorted-array/" target="_blank" rel="noopener" title="">Question</a> like Count Occurrences of a number in Sorted Array</h5>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// Question 7 : Count occurrence in Sorted array.
let ipCountArray = 
let opCountOccurance = findFirstAndLastOccurance(ipCountArray, 8)
print("opCountOccurance---",(opCountOccurance.last! - opCountOccurance.first!) + 1 ) // 3</code></pre>
<!-- /wp:code -->