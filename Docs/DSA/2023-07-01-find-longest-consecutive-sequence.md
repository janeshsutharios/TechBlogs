---
title: "Find Longest consecutive sequence"
date: 2023-07-01 13:21:07
categories: ['Array-Strings']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/longest-consecutive-sequence/description/" target="_blank" rel="noopener" title="">: </a>Given an unsorted array of integers nums, return the length of the longest consecutive elements sequence. You must write an algorithm that runs in O(n) time.<br>Example: I/P = .. Output-> 4 because 1,2,3,4 is largest consecutive.


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// Question: Find longest consecutive in an array
// TC: O(N)
// SC: O(N)
func  longestConsecutive(_ nums: ) -> Int {
    
    var setObject = Set(nums)
    var longestStreak = 0
    
    for i in 0..<nums.count {
        
        if !setObject.contains(nums - 1) {// Find smallest element in the set
            var currentNum = nums
            var currentStreak = 1
            
            while setObject.contains(currentNum + 1) {// Based on smallest element we got find next higher number
                currentNum += 1
                currentStreak += 1
            }
            
            longestStreak = max(longestStreak, currentStreak)// compare max length array
        }
    }
    
    return longestStreak
}
var consecutiveArr = 
var ansConsecutiveArr = longestConsecutive(consecutiveArr)
print("The longest consecutive sequence is ", ansConsecutiveArr)// 4</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":6} -->
<h6 class="wp-block-heading">Now a similar problem which gives consecutive array </h6>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// Question: Find longest consecutive in an array
func  longestConsecutiveArray(_ nums: ) ->  {
    
    var setObject = Set(nums)
    var longestArr: = 
    for i in 0..<nums.count {
        
        if !setObject.contains(nums - 1) {// Find smallest element in the set
            var currentNum = nums
            
            while setObject.contains(currentNum + 1) {// Based on smallest element we got find next higher number
                longestArr.append(currentNum)
                currentNum += 1
                if !setObject.contains(currentNum + 1) {
                    longestArr.append(currentNum)
                }
            }
            
        }
    }
    return longestArr
}
var consecutiveArr1 = 
var ansConsecutiveArr1 = longestConsecutiveArray(consecutiveArr1)
print("The longest consecutive sequence is ", ansConsecutiveArr1)//</code></pre>
<!-- /wp:code -->