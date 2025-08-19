---
title: "3 Sum : Find triplets that add up to a zero"
date: 2023-07-05 06:23:33
categories: ['Array-Strings']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/3sum/description/" target="_blank" rel="noopener" title="">:</a> Find triplets that add up to a zero (3 sum)<br>


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Input:</strong> nums = 
<strong>Output:</strong> ,]
<strong>Explanation:</strong> 
nums + nums + nums = (-1) + 0 + 1 = 0.
nums + nums + nums = 0 + 1 + (-1) = 0.
nums + nums + nums = (-1) + 2 + (-1) = 0.
The distinct triplets are  and .
Notice that the order of the output and the order of the triplets does not matter.</pre>
<!-- /wp:preformatted -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: O(N^3)
// SC:  O(3*k)  // k is the no.of triplets
func threeSumTrippletAddUpZero(_ nums: ) -> ] {
    let sorted = nums.sorted()// First sort the array
    var result = ]()
    for index in 0 ..< sorted.count - 2 {
        let first = sorted
        if index > 0, sorted == first {
            // Iterating through the same number. Already handled.
            continue
        }

        // Now we know the first number, iterating up from the beginning, down from the end
        // to find all cases of (second + third) == - first
        var lowerIndex = index + 1
        var upperIndex = sorted.count - 1

        /// Iterate lower bound up to change the value of `second`.
        /// Increases the sum
        func nextLower() {
            let current = sorted
            repeat {
                lowerIndex += 1
            } while lowerIndex < upperIndex && sorted == current
        }

        /// Iterate upper bound down to change the value of `third`.
        /// Decreases the sum
        func nextUpper() {
            let current = sorted
            repeat {
                upperIndex -= 1
            } while lowerIndex < upperIndex && sorted == current
        }

        while lowerIndex < upperIndex {
            let second = sorted
            let third = sorted

            switch (first + second + third) {
            case 0:
                result.append()
                nextLower()
                nextUpper()
            case ..<0:
                // We need to increase the sum
                nextLower()
            case 1...:
                // We need to decrease the sum
                nextUpper()
            default: fatalError()
            }
        }
    }
    return result
}

let sumTrippletInput = 

let opSumTripplet = threeSumTrippletAddUpZero(sumTrippletInput)
print("Output==> ", opSumTripplet) // , ]</code></pre>
<!-- /wp:code -->