---
title: "Best Time to Buy and Sell Stock"
date: 2023-06-29 13:50:02
categories: ['Array-Strings']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/best-time-to-buy-and-sell-stock/" target="_blank" rel="noopener" title="">: </a>In an array of prices where prices is the price of a given stock on an ith day. You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock. Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.


<!-- /wp:paragraph -->

<!-- wp:heading {"level":6} -->
<h6 class="wp-block-heading">Approach #1</h6>
<!-- /wp:heading -->

<!-- wp:paragraph -->
Use a buy price variable which is possibly with a max value,  difference variable is something like day when we are selling the stock (sell-buy)


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func maxProfit(arr: ) -> Int {
    var buyPrice = Int.max
    var difference = 0
    
    for i in 0..<arr.count {
        if arr < buyPrice {
            buyPrice = arr
        }
        if difference < (arr - buyPrice) {
            difference = arr - buyPrice
        }
        // OR.
        /**
        minPrice = min(minPrice, arr);
        maxPro = max(maxPro, arr - minPrice);
         */
    }
    return difference
}

var stockArray = 
let profitMax = maxProfit(arr: stockArray)
print("The maxProfit  is:", profitMax)// 5</code></pre>
<!-- /wp:code -->