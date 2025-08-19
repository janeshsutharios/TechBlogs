---
title: "How to remove duplicates from a sorted doubly linked list"
date: 2023-07-30 03:38:11
categories: ['LinkedList']
layout: post
---

<!-- wp:paragraph -->
<a href="https://www.geeksforgeeks.org/remove-duplicates-sorted-doubly-linked-list/" target="_blank" rel="noopener" title="">: </a>Given a sorted doubly linked list head.  Remove duplicate nodes from the given list.


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<strong><em>#Approach: </em></strong><br>Step 1: Compare current node item with next node item <br>Step 2: If two items same move next pointer to next's next<br>Step 3: If current Node & next Node doesn't match use node = next


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func removeDupsFromSortedDLL( _ head: DoublyLinkedListNode<Int>?) -> DoublyLinkedListNode<Int>? {    
    var node = head
    while let next = node?.next {
        if  node!.item == next.item {
            let nxtItem = next.next
            node!.next = nxtItem
            nxtItem?.previous = node
        } else {
            node = next
        }
    }
    return head
}

var sortedDLL =  DoublyLinkedList<Int>()
sortedDLL = 
let sortedDLLOutput = removeDupsFromSortedDLL(sortedDLL.head)
print("sorted DLL is--- ",sortedDLLOutput) // (1 <- -> 2 <- -> 3 <- -> 4 <- -> 9)</code></pre>
<!-- /wp:code -->