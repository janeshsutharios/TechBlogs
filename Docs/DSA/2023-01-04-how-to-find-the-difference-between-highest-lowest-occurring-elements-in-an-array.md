---
title: "How to Find the difference between highest & lowest occurring elements in an array  ?"
date: 2023-01-04 06:43:12
categories: ['Array-Strings', 'difference between min max array occurrence in swift']
layout: post
---

<!-- wp:paragraph -->
: In given array find difference between lowest & highest occurrence elements . <br>For Example: Array :   O/P = 2. because 5 appears 4 times & element 6 is 2 times. difference is 2. 


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// Question diffrence between highest & lowest occurance of a number in an array..
// TC: O(n)
// SC: O(n)
func findDiffranceBetweenHighLowOccurance(_ arr: ) -> Int {
    
    var hashObject:  = 
    for obj in arr {
        if hashObject == nil {
            hashObject = 1
        } else {
            hashObject! += 1
        }
    }
    
    let sortedObj = hashObject.sorted { $0.value > $1.value }
    if sortedObj.count > 1 {
       return sortedObj.value - sortedObj.value
    }
    return -1
}

var anArray = 
let diffrence = findDiffranceBetweenHighLowOccurance(anArray)
print("diffrence", diffrence) // 2</code></pre>
<!-- /wp:code -->