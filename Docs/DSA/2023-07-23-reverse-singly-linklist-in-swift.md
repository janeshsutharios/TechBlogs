---
title: "Reverse Singly LinkList in Swift"
date: 2023-07-23 15:20:25
categories: ['LinkedList']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/reverse-linked-list/" target="_blank" rel="noopener" title=""></a> Reverse Singly Link List using Iterative & Recursion approach.


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// Iterative Approach
func reverseList1(_ head: ListNode?) -> ListNode? {
    var prev = head, currentHead = head?.next
    prev?.next = nil
    while currentHead != nil {// At end of linked list it will be nil.
        let next = currentHead!.next
        currentHead!.next = prev
        prev = currentHead
        currentHead = next
    }
    return prev
}
// Recursive  Approach
func reverseList2(_ head: ListNode?) -> ListNode? {
    if head == nil || head?.next == nil {
        return head
    }
    let newHead = reverseList2(head?.next)
    var nextNode = head?.next
    nextNode?.next = head
    head?.next = nil
    return newHead
}</code></pre>
<!-- /wp:code -->

<!-- wp:image {"id":2066,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large">![](/TechBlogs/Assets/Website/2023/07/Reverse-LinkList-using-recuesion-878x1024.jpg)</figure>
<!-- /wp:image -->