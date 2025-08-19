---
title: "Intersection of Two Linked Lists"
date: 2023-07-25 05:52:57
categories: ['LinkedList']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/intersection-of-two-linked-lists/description/" target="_blank" rel="noopener" title="">:</a> Given the heads of two singly linked-lists <code>headA</code> and <code>headB</code>, return <em>the node at which the two lists intersect</em>. If the two linked lists have no intersection at all, return <code>null</code>.


<!-- /wp:paragraph -->

<!-- wp:image {"id":2076,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large">![](/TechBlogs/Assets/Website/2023/07/GetIntersactionNode-LinkList-1024x998.jpg)</figure>
<!-- /wp:image -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func getIntersectionNode(_ headA: ListNode?, _ headB: ListNode?) -> ListNode? {
     if headA == nil || headB == nil { return nil }
     var a = headA, b = headB
    // Where a & b node has same reference means it's a intersaction point
     while a !== b {
         a = a == nil ? headB : a?.next
         b = b == nil ? headA : b?.next
         // print("Dry run Value of a--", a, " Value of b ---", b)
     }
     // print("a", a, "b", b)
     return a
 }</code></pre>
<!-- /wp:code -->