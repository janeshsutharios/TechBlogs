---
title: "How to Find Min Max in Array"
date: 2022-11-02 07:28:20
categories: ['Array-Strings', 'DSA', 'Find Min Max of array in swift']
layout: post
---

<!-- wp:paragraph -->
  Find Maximum and minimum of an array in swift using minimum number of comparisons 


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func findMinMax(inputArray: ) -> (min:Int, max: Int) {
    if inputArray.count == 0 { return (min:-1, max: -1) }
    var minNumber = inputArray
    var maxNumber = inputArray
    for index in 1..<inputArray.count {
        if inputArray < minNumber {
            minNumber = inputArray
        }
        if inputArray > maxNumber {
            maxNumber = inputArray
        }
    }
    return (min: minNumber, max: maxNumber)
}</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":5} -->
<h5><strong><strong>#Approach: 1</strong></strong></h5>
<!-- /wp:heading -->

<!-- wp:paragraph -->
Use first element as min max & start loop from second element onwards & return tuple of the min max number


<!-- /wp:paragraph -->