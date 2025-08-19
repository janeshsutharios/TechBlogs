---
title: "Check if string is rotated"
date: 2023-07-16 04:31:53
categories: ['String']
layout: post
---

<!-- wp:paragraph -->
: Given two strings <code>s</code> and <code>goal</code>, return <code>true</code> <em>if and only if</em> <code>s</code> <em>can become</em> <code>goal</code> <em>after some number of <strong>shifts</strong> on</em> <code>s</code>.


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
A <strong>shift</strong> on <code>s</code> consists of moving the leftmost character of <code>s</code> to the rightmost position.


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
For example, if <code>s = "abcde"</code>, then it will be <code>"bcdea"</code> after one shift.


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Input:</strong> s = "abcde", goal = "abced"
<strong>Output:</strong> false</pre>
<!-- /wp:preformatted -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: O(N)
// SC: O(1)
func rotateString(_ s: String, _ goal: String) -> Bool {
    return s == goal || s.count == goal.count && (s+s).contains(goal)
}

let ipStringRot1 = "abcde"
let ipStringRot2 = "cdeab"

let opStringRot = rotateString(ipStringRot1, ipStringRot2)
print("op is-- ", opStringRot)// true</code></pre>
<!-- /wp:code -->