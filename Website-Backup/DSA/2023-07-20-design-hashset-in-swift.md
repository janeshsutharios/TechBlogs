---
title: "Design Hashset in swift"
date: 2023-07-20 15:47:26
categories: ['LinkedList']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/design-hashset/description/" target="_blank" rel="noopener" title="">: </a>Design a HashSet without using any built-in hash table libraries.


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
Implement <code>MyHashSet</code> class:


<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><!-- wp:list-item -->
<li><code>void add(key)</code> Inserts the value <code>key</code> into the HashSet.</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li><code>bool contains(key)</code> Returns whether the value <code>key</code> exists in the HashSet or not.</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li><code>void remove(key)</code> Removes the value <code>key</code> in the HashSet. If <code>key</code> does not exist in the HashSet, do nothing.</li>
<!-- /wp:list-item --></ul>
<!-- /wp:list -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">class MyHashSet {
     private var data = (repeating: false, count: 1000001)
     init() {}
     func add(_ key: Int) { data = true }
     func remove(_ key: Int) { data = nil }
     func contains(_ key: Int) -> Bool { data ?? false }
}
// Bitwise Solution: --
class MyHashSet2 {
    private var bits =  (repeating: 0, count: 1000001) // 15_626 = 1_000_000 / 64 + 1
    func add(_ key: Int) { bits |= 1<<(key&63) }
    func remove(_ key: Int) { bits &= ~(1<<(key&63)) }
    func contains(_ key: Int) -> Bool { bits & 1<<(key&63) != 0 }
}</code></pre>
<!-- /wp:code -->