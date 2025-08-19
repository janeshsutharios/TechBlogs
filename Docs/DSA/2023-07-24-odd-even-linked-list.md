---
title: "Odd Even Linked List"
date: 2023-07-24 07:12:33
categories: ['LinkedList']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/odd-even-linked-list/description/" target="_blank" rel="noopener" title=""> </a>Given the <code>head</code> of a singly linked list, group all the nodes with odd indices together followed by the nodes with even indices, and return <em>the reordered list</em>.


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
The <strong>first</strong> node is considered <strong>odd</strong>, and the <strong>second</strong> node is <strong>even</strong>, and so on.


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
You must solve the problem in <code>O(1)</code> extra space complexity and <code>O(n)</code> time complexity.


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<strong>Example 1:</strong>


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Input:</strong> head = 
<strong>Output:</strong> </pre>
<!-- /wp:preformatted -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func oddEvenList(_ head: ListNode?) -> ListNode? {
    var oddHead = head
    var evenHead = head?.next
    var evenOrignalHead = head?.next
    while evenHead != nil && evenHead?.next != nil {
        oddHead?.next = evenHead?.next // Step A
        oddHead = oddHead?.next // Step B
        evenHead?.next = oddHead?.next// Step C
        evenHead = evenHead?.next// Step D
    }
    oddHead?.next = evenOrignalHead // Step E
    return head
}</code></pre>
<!-- /wp:code -->

<!-- wp:image {"id":2072,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large">![](/TechBlogs/Assets/Website/2023/07/Odd-even-linked-list-853x1024.jpg)</figure>
<!-- /wp:image -->