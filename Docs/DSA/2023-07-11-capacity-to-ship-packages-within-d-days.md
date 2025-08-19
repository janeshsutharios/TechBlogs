---
title: "Capacity To Ship Packages Within D Days"
date: 2023-07-11 10:52:52
categories: ['BinarySearch']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/description/" target="_blank" rel="noopener" title="">: </a>A conveyor belt has packages that must be shipped from one port to another within <code>days</code> days.The <code>i<sup>th</sup></code> package on the conveyor belt has a weight of <code>weights</code>. Each day, we load the ship with packages on the conveyor belt (in the order given by <code>weights</code>). We may not load more weight than the maximum weight capacity of the ship.Return the least weight capacity of the ship that will result in all the packages on the conveyor belt being shipped within <code>days</code> days.


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<strong>Example 1:</strong>


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Input:</strong> weights = , days = 5
<strong>Output:</strong> 15
<strong>Explanation:</strong> A ship capacity of 15 is the minimum to ship all the packages in 5 days like this:
1st day: 1, 2, 3, 4, 5
2nd day: 6, 7
3rd day: 8
4th day: 9
5th day: 10

Note that the cargo must be shipped in the order given, so using a ship of capacity 14 and splitting the packages into parts like (2, 3, 4, 5), (1, 6, 7), (8), (9), (10) is not allowed.
</pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<strong>Example 2:</strong>


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Input:</strong> weights = , days = 3
<strong>Output:</strong> 6
<strong>Explanation:</strong> A ship capacity of 6 is the minimum to ship all the packages in 3 days like this:
1st day: 3, 2
2nd day: 2, 4
3rd day: 1, 4</pre>
<!-- /wp:preformatted -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: O(Nlog(N))
// SC: O(1)
func feasible(_ weights: ,_ c: Int, _ days: Int) ->Bool {
    var daysNeeded = 1, currentLoad = 0
    for weight in weights {
        currentLoad += weight
        if currentLoad > c {// if current load exceeds capacity
            daysNeeded += 1
            currentLoad = weight
        }
    }
    
    return daysNeeded <= days
}

func shipWithinDays(_ weights: ,_ days: Int) ->Int {
    var totalLoad = 0, maxLoad = 0
    for weight in weights {
        totalLoad += weight
        maxLoad = max(maxLoad, weight)// Max load will be highest element in the array
    }
    
    var l = maxLoad, r = totalLoad
    
    while l < r {
        var mid = (l + r) / 2
        if feasible(weights, mid, days) {
            r = mid
        } else {
            l = mid + 1
        }
    }
    return l
}

let ipShipWeightArray = 
let shipDays = 5
let opLeastWeight = shipWithinDays(ipShipWeightArray, shipDays)
print("opLeastWeight--- ", opLeastWeight)// 15</code></pre>
<!-- /wp:code -->