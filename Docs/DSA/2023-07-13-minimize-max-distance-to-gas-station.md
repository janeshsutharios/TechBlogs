---
title: "Minimize Max Distance to Gas Station"
date: 2023-07-13 07:45:09
categories: ['BinarySearch']
layout: post
---

<!-- wp:paragraph -->
<a href="https://practice.geeksforgeeks.org/problems/minimize-max-distance-to-gas-station/1" target="_blank" rel="noopener" title=""> </a>We have an horizontal number line. On that number line, we have gas <strong>stations </strong>at positions stations, stations, ..., stations, where <strong>N </strong>= size of the stations array. Now, we add <strong>K</strong> more gas stations so that <strong>D</strong>, the maximum distance between adjacent gas stations, is minimized. We have to find the smallest possible value of D. Find the answer <strong>exactly</strong> to 2 decimal places.


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<strong>Example 1:</strong>


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Input:
</strong>N = 10
stations = 
K = 9
<strong>Output:</strong> 0.50
<strong>Explanation: </strong>Each of the 9 stations can be added mid way between all the existing adjacent stations.</pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<strong>Example 2:</strong>


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Input:
</strong>N = 10
stations = <code></code>
K = 2
<strong>Output:</strong> 14.00</pre>
<!-- /wp:preformatted -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: O(Nlog(N))
// SC: O(1)
func isPossibleToPlace(_ stations: ,_ x: Double) -> Int {
    var station_count = 0
    for i in 0..<stations.count - 1 {
        let distance = Double(stations - stations)
        station_count += Int(ceil(distance / x)) - 1
    }
    return station_count
}

func findSmallestMaxDist(_ stations: , _ k: Int) ->Double {
    // Code here
    var low = 0.0;
    var n = stations.count
    var high = Double(stations - stations)
    while (high - low) > 0.000001 {
        var mid = Double(low + high) / 2
        var x = isPossibleToPlace(stations, mid)
        if x > k {
            low = mid
        } else {
            high = mid
        }
    }
    return high
}

let gasStationArray = 
let gasStationToBeInsert = 2
let gasStationDistance = findSmallestMaxDist(gasStationArray, gasStationToBeInsert)
print(" gasStationDistance -- ", gasStationDistance)// 14</code></pre>
<!-- /wp:code -->

<!-- wp:image {"id":1989,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large">![](/TechBlogs/Assets/Website/2023/07/Max-distance-gas-station-937x1024.jpeg)</figure>
<!-- /wp:image -->