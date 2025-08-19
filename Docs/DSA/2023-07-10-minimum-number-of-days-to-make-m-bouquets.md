---
title: "Minimum Number of Days to Make m Bouquets"
date: 2023-07-10 12:48:46
categories: ['BinarySearch']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/minimum-number-of-days-to-make-m-bouquets/description/" target="_blank" rel="noopener" title=""></a> In an integer array <code>bloomDay</code>, an integer <code>m</code> and an integer <code>k</code>.You want to make <code>m</code> bouquets. To make a bouquet, you need to use <code>k</code> <strong>adjacent flowers</strong> from the garden. The garden consists of <code>n</code> flowers, the <code>i<sup>th</sup></code> flower will bloom in the <code>bloomDay</code> and then can be used in <strong>exactly one</strong> bouquet.


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
Return <em>the minimum number of days you need to wait to be able to make </em><code>m</code><em> bouquets from the garden</em>. If it is impossible to make m bouquets return <code>-1</code>.


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<strong>Example 1:</strong>


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Input:</strong> bloomDay = , m = 3, k = 1
<strong>Output:</strong> 3
<strong>Explanation:</strong> Let us see what happened in the first three days. x means flower bloomed and _ means flower did not bloom in the garden.
We need 3 bouquets each should contain 1 flower.
After day 1:    // we can only make one bouquet.
After day 2:    // we can only make two bouquets.
After day 3:    // we can make 3 bouquets. The answer is 3.</pre>
<!-- /wp:preformatted -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">//TC: O(log(max(arr)-min(arr)+1) * N), where {max(arr) -> maximum element of the array, min(arr) -> minimum element of the array, N = size of the array}.
// Reason: We are applying binary search on our answers that are in the range of ), max(arr)]. For every possible answer ‘mid’, we will call the possible() function. Inside the possible() function, we are traversing the entire array, which results in O(N).
// SC: O(1)

func minDays(_ bloomDay: , _ m: Int, _ k: Int) -> Int {
    
    func possible(_ bloomDay: , _ day: Int,_ m: Int,_ k: Int) -> Bool {
        var cnt = 0;
        var noOfB = 0;
        // Count the number of bouquets
        for i in 0..<bloomDay.count {
            if bloomDay <= day {
                cnt+=1;
            } else {
                noOfB += Int(floor(Double(cnt / k)))
                cnt = 0;
            }
        }
        noOfB += Int(floor(Double(cnt / k)))
        return noOfB >= m
    }
    
    let val = m * k;
    if (val > bloomDay.count) {
        return -1
    } // Impossible case
    // Find maximum and minimum
    var mini = 0, maxi = 0;
    for i in 0..<bloomDay.count {
        mini = min(mini, bloomDay);
        maxi = max(maxi, bloomDay);
    }
    
    // Apply binary search
    var low = mini, high = maxi;
    while low <= high {
        let mid = Int(floor(Double(low + high) / 2))
        if (possible(bloomDay, mid, m, k)) {
            high = mid - 1;
        } else {
            low = mid + 1;
        }
    }
    return low;
}

let bonqutesArr = ;
let adjacentRosesRequired = 3;
let totalBouquets = 2;// , 
let minDaysOP = minDays(bonqutesArr, totalBouquets, adjacentRosesRequired);
print("We can make bouquets on day ", minDaysOP);// day 12 so it will be  & 

</code></pre>
<!-- /wp:code -->