---
title: "Merge all overlapping intervals"
date: 2023-07-06 10:55:24
categories: ['Array-Strings']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/merge-intervals/description/" target="_blank" rel="noopener" title="">: </a>Given an array of <code>intervals</code> where <code>intervals = </code>, merge all overlapping intervals, and return <em>an array of the non-overlapping intervals that cover all the intervals in the input</em>.<br>Example: - 


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Input:</strong> intervals = ,,,]
<strong>Output:</strong> ,,]
<strong>Explanation:</strong> Since intervals  and  overlap, merge them into .

<strong><em>Constraints:
</em></strong>1 <= intervals.length <= 104
intervals.length == 2
0 <= starti <= endi <= 104</pre>
<!-- /wp:preformatted -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">//Time Complexity: O(N*logN) + O(N), where N = the size of the given array.
//Reason: Sorting the given array takes  O(N*logN) time complexity. Now, after that, we are just using a single loop that runs for N times. So, the time complexity will be O(N).
//Space Complexity: O(N), as we are using an answer list to store the merged intervals. Except for the answer array, we are not using any extra space.
func mergeOverlappingIntervals(_ intervals: ]) -> ] {
    
    guard !intervals.isEmpty else { return  }
    var intervals = intervals.sorted(by: { $0 < $1 })// We are sorting the array hence we get sorted intervals
    
    var ans = ]() // Answer stored
    var start = intervals // First object
    var end = intervals // First object
    
    for interval in intervals {
        if end < interval {
            ans.append()
            start = interval
            end = interval
        } else {
            end = max(end, interval)// Increment end till we get max
        }
    }
    
    ans.append()
    return ans
}

let arrMergeIntervals = , , , ];
var ansMergeInterals = mergeOverlappingIntervals(arrMergeIntervals);
print("The merged intervals are:", ansMergeInterals) // , , ]</code></pre>
<!-- /wp:code -->