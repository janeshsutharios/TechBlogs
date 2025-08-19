---
title: "Delete Middle node from Single Link List"
date: 2023-07-21 11:36:17
categories: ['LinkedList']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/delete-the-middle-node-of-a-linked-list/description/" target="_blank" rel="noopener" title="">:</a> You are given the <code>head</code> of a linked list. <strong>Delete</strong> the <strong>middle node</strong>, and return <em>the</em> <code>head</code> <em>of the modified linked list</em>.


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
The <strong>middle node</strong> of a linked list of size <code>n</code> is the <code>⌊n / 2⌋<sup>th</sup></code> node from the <strong>start</strong> using <strong>0-based indexing</strong>, where <code>⌊x⌋</code> denotes the largest integer less than or equal to <code>x</code>.


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func deleteMiddle(_ head: ListNode?) -> ListNode? {
     if head?.next == nil {
         return nil
     }
     var slowPointer = head // 1X time mover
     var fastPointer = head// 2X mover
     var prevNode: ListNode?// This is middle - 1 Node
     while fastPointer?.next != nil {
         fastPointer = fastPointer?.next?.next
         prevNode = slowPointer
         slowPointer = slowPointer?.next
     }
     prevNode?.next = slowPointer?.next// middle Node - 1 next's is middle + 1 node
     return head
 }

var aLinkList = ListNode(1, ListNode(2, ListNode(3)))
aLinkList = deleteMiddle(aLinkList)!
print("After Deleting Link list will look like--", aLinkList) //  1 -> 3 </code></pre>
<!-- /wp:code -->