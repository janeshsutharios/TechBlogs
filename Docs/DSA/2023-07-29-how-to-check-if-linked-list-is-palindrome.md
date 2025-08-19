---
title: "How to check if linked list is palindrome?"
date: 2023-07-29 17:27:34
categories: ['LinkedList']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/palindrome-linked-list/" target="_blank" rel="noopener" title="">: </a>Input singly linked list return true if linked list is palindrome.<br>Example: -


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Input:</strong> head = 
<strong>Output:</strong> true</pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<strong><em>Approach#</em> </strong>Reverse Linked list & compare first and last item


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func reverseList2(_ head: ListNode?) -> ListNode? {
     if head == nil || head?.next == nil {
         return head
     }
     let newHead = reverseList2(head?.next)
     let nextNode = head?.next
     nextNode?.next = head
     head?.next = nil
     return newHead
 }
 
 func isPalindrome(_ head: ListNode?) -> Bool {
     if head == nil {
         return true
     }
     var headCopy = head
     var middleNode = findMiddle(head)
     middleNode = reverseList2(middleNode)
     while middleNode != nil {
         if headCopy?.val != middleNode?.val {
             return false
         }
         headCopy = headCopy?.next
         middleNode = middleNode?.next
     }
     return true
 }

 func findMiddle(_ head: ListNode?) -> ListNode? {
     var slow = head, fast = head
     while fast?.next != nil && fast != nil {
         slow = slow?.next
         fast = fast?.next?.next
     }
     return slow
 }

var palindromeLinkedList = ListNode(5, ListNode(1, ListNode(10,ListNode(1, ListNode(5)))))
let isPalindrom = isPalindrome(palindromeLinkedList)
//print("LinkList isPalindrom --- ", isPalindrom) // true</code></pre>
<!-- /wp:code -->