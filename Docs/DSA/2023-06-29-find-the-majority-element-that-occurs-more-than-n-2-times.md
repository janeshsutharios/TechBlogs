---
title: "Find the Majority Element that occurs more than N/2 times"
date: 2023-06-29 12:26:50
categories: ['Array-Strings']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/majority-element/description/" target="_blank" rel="noopener" title=""></a> Find the Majority Element in an given array that occurs more than N/2 times


<!-- /wp:paragraph -->

<!-- wp:heading {"level":6} -->
<h6 class="wp-block-heading">Approach #1 Brute-force  </h6>
<!-- /wp:heading -->

<!-- wp:paragraph -->
Use two loop and compare each elements with rest if it matches increment the counter 


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: O(n*2)
// SC: O(1)
func majorityElement(arr: inout ) -> Int {
    // Size of the given array
    let n = arr.count

    for i in 0..<n {
        // Selected element is arr
        var cnt = 0
        for j in 0..<n {
            // Counting the frequency of arr
            if arr == arr {
                cnt+=1
            }
        }
        
        // Check if frequency is greater than n/2
        if (cnt > n/2) {
            return arr
        }
    }

    return -1
}</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":6} -->
<h6 class="wp-block-heading">Approach #2 : Optimal Approach: Moore’s Voting Algorithm</h6>
<!-- /wp:heading -->

<!-- wp:paragraph -->
 Basically, we are trying to keep track of the occurrences of the majority element and minority elements dynamically. if the count becomes 0 as the occurrence of Element and the occurrence of the other elements are the same. So, they canceled each other. The element with the most occurrence will remain and the rest will cancel themselves.


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func majorityElementMooreVoting(arr: inout ) -> Int {
    // Size of the given array
    let n = arr.count
    var cnt = 0 // Count
    var el = 0 // Element

    // Applying the algorithm
    for i in 0..<n {
        if cnt == 0 {
            cnt = 1
            el = arr
        } else if el == arr {
            cnt+=1
        } else {
            cnt-=1
        }
    }

    // Checking if the stored element is the majority element
    var cnt1 = 0
    for i in 0..<n where arr == el {
        cnt1+=1
    }

    if (cnt1 > n / 2) {
        return el
    }
    return -1
}</code></pre>
<!-- /wp:code -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">var majorityArr = 
let ansMajority = majorityElementMooreVoting(arr: &majorityArr)
print("The majority element is:", ansMajority)</code></pre>
<!-- /wp:code -->