---
title: "How to print n times using recursion"
date: 2022-11-12 14:46:01
categories: ['print using recursion in swift', 'Recursion']
layout: post
---

<!-- wp:paragraph -->
So here we have used recursion The names which is before function will print FIFO & vice versa 


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func printNTimes(i: Int, n: Int) {
    if i > n {
        print("invalid,", i)
        return
    }
    print("Before-->", i)
    printNTimes(i: i+1, n: n)
    print("After-->", i)
}
print("Printing...")
printNTimes(i: 1, n: 5)
// It will print
Printing...
Before--> 1
Before--> 2
Before--> 3
Before--> 4
Before--> 5
invalid, 6
After--> 5
After--> 4
After--> 3
After--> 2
After--> 1
</code></pre>
<!-- /wp:code -->