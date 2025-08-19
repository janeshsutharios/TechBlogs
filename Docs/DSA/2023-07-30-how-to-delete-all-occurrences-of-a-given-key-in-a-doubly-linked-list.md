---
title: "How to Delete all occurrences of a given key in a doubly linked list"
date: 2023-07-30 03:21:28
categories: ['LinkedList']
layout: post
---

<!-- wp:paragraph -->
<a href="https://www.geeksforgeeks.org/delete-occurrences-given-key-doubly-linked-list/" target="_blank" rel="noopener" title="">: </a>Given a doubly linked list and a key <strong>x</strong>. The problem is to delete all occurrences of the given key <strong>x</strong> from the doubly linked list.


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<strong><em>#Approach: </em></strong>we declare two variable prevNode and nxtNode and in a loop if we finds the data value of linklist node is equals to k just break link to the node.


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func deleteOccuranceInLinkedList(_ k: Int, _ list: DoublyLinkedListNode<Int>?) -> DoublyLinkedListNode<Int>? {
    
    var tempCopy = list
    
    while tempCopy != nil {
        var prevNode = tempCopy?.previous
        var nxtNode = tempCopy?.next

        if tempCopy?.item == k {
            prevNode?.next = nxtNode
            nxtNode?.previous = prevNode
        }
        tempCopy = tempCopy?.next
    }
    return tempCopy
}

var occuranceLinkedList = DoublyLinkedList<Int>()
occuranceLinkedList  = 
deleteOccuranceInLinkedList(2, occuranceLinkedList.head)
//print(" after deleting k linked list is", occuranceLinkedList)// 1,3,1,4,5</code></pre>
<!-- /wp:code -->