---
title: "Aggressive Cows : Detailed Solution"
date: 2023-07-12 06:45:31
categories: ['BinarySearch']
layout: post
---

<!-- wp:paragraph -->
<a href="https://takeuforward.org/data-structure/aggressive-cows-detailed-solution/" target="_blank" rel="noopener" title="">: </a>Given an array of length ‘N’, where each element denotes the position of a stall. Now you have ‘N’ stalls and an integer ‘K’ which denotes the number of cows that are aggressive. To prevent the cows from hurting each other, you need to assign the cows to the stalls, such that the minimum distance between any two of them is as large as possible. Return the largest minimum distance.<br>Eg -


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">array: 1,2,4,8,9  &  k=3
O/P: 3
Explanation: 1st cow at stall 1 , 2nd cow at stall 4 and 3rd cow at stall 8// One integer, the largest minimum distance 3</code></pre>
<!-- /wp:code -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong> </strong></pre>
<!-- /wp:preformatted -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: O(Nlog(N))
// SC: O(1)
func isPossibleToPlace(_ stallArray: ,_ numberOfStalls:Int, _ cows: Int, _ minDist: Int) -> Bool {
    var cntCows = 1
    var lastPlacedCow = stallArray// The first position of cow
    for  i in 1..<numberOfStalls {
        if stallArray - lastPlacedCow >= minDist {// As we need largest distace
            cntCows += 1
            lastPlacedCow = stallArray// change position of cow
        }
    }
    if cntCows >= cows {// If cows in stall matches with the inut cows count...
        return true
    }
    return false
}

func aggresiveCowPlaces(_ stallArray: , _ cows: Int) -> Int {
    if stallArray.isEmpty { return -1 }
    var sortedCowsArr = stallArray.sorted()
    var cowPosition = sortedCowsArr
    let numberOfStalls = sortedCowsArr.count
    var low = 1 // the first index
    var high = sortedCowsArr - sortedCowsArr // high is max value in stall array
    
    while low <= high {
        let mid = (low + high) >> 1;
        if isPossibleToPlace(sortedCowsArr, numberOfStalls, cows, mid) {
            low = mid + 1 // discard left half of array
        } else {
            high = mid - 1 // discard right half of array
        }
    }
    return high
}

var cows = 3
var cowsStalls = 

let minDistanceCows = aggresiveCowPlaces(cowsStalls, cows)
print("< -- minDistanceCows -- >", minDistanceCows) // 3</code></pre>
<!-- /wp:code -->