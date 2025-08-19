---
title: "Koko eating Banana || Return min value using Binary search"
date: 2023-07-10 10:37:38
categories: ['BinarySearch']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/koko-eating-bananas/description/" target="_blank" rel="noopener" title="">: </a> There are <code>n</code> piles of bananas, the <code>i<sup>th</sup></code> pile has <code>piles</code> bananas. The guards have gone and will come back in <code>h</code> hours.<br>Koko can decide her bananas-per-hour eating speed of <code>k</code>. Each hour, she chooses some pile of bananas and eats <code>k</code> bananas from that pile. If the pile has less than <code>k</code> bananas, she eats all of them instead and will not eat any more bananas during this hour. Koko likes to eat slowly but still wants to finish eating all the bananas before the guards return. Return <em>the minimum integer</em> <code>k</code> <em>such that she can eat all the bananas within</em> <code>h</code> <em>hours</em>.


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<strong>Example 1:</strong>


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Input:</strong> piles = , h = 8
<strong>Output:</strong> 4</pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<strong>Example 2:</strong>


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Input:</strong> piles = , h = 5
<strong>Output:</strong> 30</pre>
<!-- /wp:preformatted -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: O(n log k)
//  O(n)(checkHours) * O(log k)(binary search where k = piles(max))
// SC: O(1) only a few integers are stored.

func checkHours(_ piles: , _ k: Int, _ limit: Int) -> Bool {
     var hours = 0
     for pile in piles {
         hours += Int(ceil(Double(pile) / Double(k)))
         if hours > limit {// If hour limit exceeds means discard right half of array
             return false
         }
     }
     return hours <= limit
 }
 
 func minEatingSpeed(_ piles: , _ h: Int) -> Int {
     // Define the binary search space,
     // 1...max(piles) in this case.
     var left = 1, right = Int.min
     for pile in piles {
         right = max(right, pile)
     }
     
     while left <= right {
         let mid = (left + right) / 2
         if checkHours(piles, mid, h) {
             // Koko eats too many bananas.
             // Encourage Koko to eat less bananas per hour.
             right = mid - 1
             // Discard right half of array
         } else {
             // Koko doesn't eat enough banans.
             // Ask Koko to eat one more banana per hour.
             left = mid + 1
             // Discard left half of array
         }
     }
     
     return left
 }
let v = 
let h = 8
let ans = minEatingSpeed(v, h)
print("Koko should eat at least ", ans, " bananas/hr.")// 4</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":5} -->
<h5 class="wp-block-heading">#Approach 2: Using reduce</h5>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func minEatingSpeed1(_ piles: , _ h: Int) -> Int {
    var (l, r) = (1, piles.max()!)
    while l < r{
        var k = (l + r) / 2
        let hrs = piles.reduce(0){return $0 + ($1 + k - 1)/k}
        (l, r) = hrs <= h ? (k-1, k) : (k+1, r)
    }
    return l
}</code></pre>
<!-- /wp:code -->