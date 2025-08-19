---
title: "Sort Characters By Frequency"
date: 2023-07-17 04:53:54
categories: ['String']
layout: post
---

<!-- wp:paragraph -->
: Given a string <code>s</code>, sort it in <strong>decreasing order</strong> based on the <strong>frequency</strong> of the characters. for example "tree" so ee has highest appearance hence answer will be eert


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
Return <em>the sorted string</em>. If there are multiple answers, return <em>any of them</em><br><strong>Input:</strong> s = "tree"<br><strong>Output:</strong> "eert"


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: O(N)
// SC: O(N)
func frequencySort(_ s: String) -> String {
    var dict: = 
    for c in s {
        dict += String(c)
    }
    //        var sortedDictionary = dict.sorted { (aDic, bDic) -> Bool in
    //            return aDic.value.count > bDic.value.count
    //        }
    // Here we can also use some sorting technique, like merge sort
    var sortedDictionary = dict.sorted {
        $0.1.count > $1.1.count
    }
    var ans = ""
    for (_, value) in sortedDictionary {
        ans += value
    }
    return ans
}
//Other Solution using high order functions.
/*
func frequencySort(_ s: String) -> String {
    let counts = s.reduce(into: ) {$0 += 1}
    let sortedCounts = counts.sorted(by: { $0.value > $1.value })
    return sortedCounts.reduce(into: "") {$0.append(
        String(repeating: $1.0, count: $1.1))
    }
}
func frequencySort(_ s: String) -> String {
    return Dictionary(s.map { ($0, 1)}, uniquingKeysWith: +)
        .sorted(by: { $0.value > $1.value })
        .reduce("") { $0 + String(repeating: $1.key, count: $1.value) }
}
 func frequencySort(_ s: String) -> String {
     var dic = ()
     var ans = ""
     
     s.map{ dic += String($0) }
     dic.sorted{ $0.1.count > $1.1.count }.map{ ans += $0.1 }
     
     return ans
 }
*/
 
let strObj = "tree"
let opSortedStr = frequencySort(strObj)
print(" opSortedStr-- ", opSortedStr)// eert
</code></pre>
<!-- /wp:code -->