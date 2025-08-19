---
title: "How to log a method's execution time in Xcode ?"
date: 2022-11-26 15:35:58
categories: ['cfabsolutetimegetcurrent', 'iOS', 'Swift', 'swift measure execution time']
layout: post
---

<!-- wp:paragraph -->
We often required to calculate how much time xcode required for execute certain chunk of code. Fortunately there is a workaround  which might be used is <strong><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">`CFAbsoluteTimeGetCurrent()`</mark></strong>Here i have used Big O(n^2) Time complexity you can change values & test it over xcode.


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">let startTime = CFAbsoluteTimeGetCurrent()
// run your work
func tempFunction(_ s: String) -> String {
    for _ in 0..<999 {
        for _ in 0..<9999 {}
    }
    return "Got it"
}
print(tempFunction("123"))
let diffrence = CFAbsoluteTimeGetCurrent() - startTime
print("It required \(diffrence) seconds") // 4.7849119901657104</code></pre>
<!-- /wp:code -->