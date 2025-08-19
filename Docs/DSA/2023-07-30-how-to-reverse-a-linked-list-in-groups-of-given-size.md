---
title: "How to Reverse a Linked List in groups of given size"
date: 2023-07-30 04:03:24
categories: ['LinkedList']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/reverse-nodes-in-k-group/" target="_blank" rel="noopener" title="">: </a>Given the <code>head</code> of a linked list, reverse the nodes of the list <code>k</code> at a time, and return <em>the updated list</em>. <code>k</code> is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of <code>k</code> then left-out nodes, in the end, should remain as it is.


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
Criteria: Don't alter the values in the list's nodes, only nodes themselves may be changed.<br>Example:- <br><strong>Input</strong><em>: 1->2->3->4->5->6->7->8->NULL, K = 3 </em><br><strong>Output</strong><em>: 3->2->1->6->5->4->8->7->NULL </em>


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<strong><em>Approach#</em></strong> Recursive solution. curr node points to k+1 now reverse the nodes with the subset.


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func reverseKGroup(_ head: ListNode?, _ k: Int) -> ListNode? {
    var curr = head
    var headyCopy = head
    var count = 0
    while curr != nil && count != k {// Find K+1 Node
        curr = curr?.next
        count+=1
    }
    if count == k {// if k+1 node is found
        curr = reverseKGroup(curr,k)// reverse list with k+1 node as head
        // headCopy - head-pointer to direct part,
        // curr - head-pointer to reversed part
        while count > 0 {// reverse current k-group:
            var tmp = headyCopy?.next // tmp - next head in direct part
            headyCopy?.next = curr// preappending "direct" headCopy to the reversed list
            curr = headyCopy // move head of reversed part to a new node
            headyCopy = tmp // move "direct" headCopy to the next node in direct part
            count-=1
        }
        headyCopy = curr
    }
    return headyCopy
}

let kGroupLinkedListInput = ListNode(1, ListNode(2, ListNode(3,ListNode(4, ListNode(5)))))
let kGroupLinkedListOutput = reverseKGroup(kGroupLinkedListInput, 2)
print("Output of kth nummber reversed linked list is ---", kGroupLinkedListOutput!)// 2 1 4 3 5</code></pre>
<!-- /wp:code -->