---
title: "How to add attributed string swift ?"
date: 2022-12-12 12:25:43
categories: ['attributed string with different fonts swift', 'convert string to attributed string swift', 'how to make part of a string bold in swift', 'iOS', 'label with two different colors swift', 'Swift', 'swift attributed string example', 'uilabel text different color', 'uilabel with different font sizes swift']
layout: post
---

<!-- wp:paragraph -->
If you have two diffrent string  and want to have diffrent text style like colours, font then you can use <mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">NSAttributedString</mark> which can customise. In below example i have joined two string with diffrent fonts,  colours into same label.


<!-- /wp:paragraph -->

<!-- wp:image {"id":1614,"width":865,"height":351,"sizeSlug":"full","linkDestination":"none"} -->
<figure class="wp-block-image size-full is-resized">![](/TechBlogs/Assets/Website/2022/12/Attribute-String-in-swift-1.png)</figure>
<!-- /wp:image -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">let mutableString = NSMutableAttributedString()
let attributedString = NSAttributedString(string:"Helllo... ",
                                   attributes:[NSAttributedString.Key.foregroundColor: UIColor.blue,
                                               NSAttributedString.Key.font: UIFont.systemFont(ofSize: 22) as Any])
mutableString.append(attributedString)
let attributedString2 = NSAttributedString(string:"Janesh",
                                   attributes:[NSAttributedString.Key.foregroundColor: UIColor.red,
                                               NSAttributedString.Key.font: UIFont.boldSystemFont(ofSize: 30) as Any])
mutableString.append(attributedString2)

self.lbl.attributedText = mutableString</code></pre>
<!-- /wp:code -->