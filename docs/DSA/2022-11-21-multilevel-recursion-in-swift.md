---
title: "Multilevel recursion in swift"
date: 2022-11-21 10:52:10
categories: ['DSA', 'learn recursion in ios', 'learn recursion in swift', 'Recursion', 'recursion in swift']
layout: post
---

<!-- wp:paragraph -->
Here we will discuss two level recursion in swift. If there is statement before the recursive function it will print in sequence & vice versa. Here is example code with print statement - 


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func test(currentIndex: Int) {
    if currentIndex > 2 {
        print("exit")
        return
    }
    print("before", currentIndex)
    test(currentIndex: currentIndex+1)
    print("after------- ", currentIndex)
    test(currentIndex: currentIndex+1)
    print("Final ================  ", currentIndex)
    
}

test(currentIndex: 0)</code></pre>
<!-- /wp:code -->

<!-- wp:image {"id":1544,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large">![](/TechBlogs/Assets/Website/2022/11/Recursion-tree-957x1024.jpg)</figure>
<!-- /wp:image -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">Prints-- > 
before 0
before 1
before 2
exit
after-------  2
exit
Final ================   2
after-------  1
before 2
exit
after-------  2
exit
Final ================   2
Final ================   1
after-------  0
before 1
before 2
exit
after-------  2
exit
Final ================   2
after-------  1
before 2
exit
after-------  2
exit
Final ================   2
Final ================   1
Final ================   0</code></pre>
<!-- /wp:code -->