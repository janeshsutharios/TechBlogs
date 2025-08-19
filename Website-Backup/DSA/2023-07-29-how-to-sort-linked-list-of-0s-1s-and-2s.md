---
title: "How to Sort linked list of 0s, 1s and 2s"
date: 2023-07-29 17:47:49
categories: ['LinkedList']
layout: post
---

<!-- wp:paragraph -->
<a href="https://www.geeksforgeeks.org/sort-a-linked-list-of-0s-1s-or-2s/" target="_blank" rel="noopener" title="">: </a>Given a singly linked list head sort it with with all with zeros, ones and two's<br>Example:<br><strong>Input:</strong><em> 1 -> 1 -> 2 -> 0 -> 2 -> 0 -> 1 -> NULL </em><br><strong>Output:</strong><em> 0 -> 0 -> 1 -> 1 -> 1 -> 2 -> 2 -> NULL</em>


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<strong><em>Approach:</em></strong> Create count array which stores count of 0's, 1's and 2's occurrences. We will iterate over linked list & finds the count of each(0,1,2) <br>Create a new head named `current` and replace items with sorted order


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: O(n)
// SC: O(n)
func sortList012(_ head: ListNode?) {
    var count = 
    // Count the number of 0's, 1's, and 2's in the
    // linked list
    var current = head
    while current != nil {
        count+=1// Filling respective index like count of 0's 1's & 2's
        current = current?.next
    }
    // Overwrite the linked list with the sorted
    // elements
    current = head
    var i = 0
    while current != nil {
        if count == 0 {
            i+=1
        } else {
            current?.val = i
            count-=1
            current = current?.next
        }
    }
}

let zeroOneTwoLinkedList = ListNode(1, ListNode(2, ListNode(0,ListNode(2, ListNode(0)))))
sortList012(zeroOneTwoLinkedList)
//print("sorted by 0,1,2", zeroOneTwoLinkedList)// 0 0 1 2 1</code></pre>
<!-- /wp:code -->