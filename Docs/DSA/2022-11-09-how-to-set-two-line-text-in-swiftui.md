---
title: "How to set two line text in SwiftUI ?"
date: 2022-11-09 13:11:31
categories: ['iOS', 'Set two lines text in swiftUI', 'SwiftUI']
layout: post
---

<!-- wp:paragraph -->
For setting up n number of lines of Text in swiftUI we can use <a href="https://developer.apple.com/documentation/swiftui/text/linelimit(_:)-shpb" target="_blank" rel="noopener" title="">.lineLimit</a>(..   function which takes arguments as number of lines.


<!-- /wp:paragraph -->

<!-- wp:heading {"level":4,"textColor":"ast-global-color-1"} -->
<h4 class="has-ast-global-color-1-color has-text-color">#For iOS 15 & Below : </h4>
<!-- /wp:heading -->

<!-- wp:paragraph -->
we have to set <code>.fixedSize(horizontal: false, vertical: true)</code> &    <code> .lineLimit(2)</code>


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">Text("A two lines TextABCDEFGHIJKLMNOPQRSTUVWXYZ 1234567890 All alphabates")
    .fixedSize(horizontal: false, vertical: true)
    .lineLimit(2)</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":4,"textColor":"ast-global-color-1"} -->
<h4 class="has-ast-global-color-1-color has-text-color"># For iOS 16 onwards</h4>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">Text("A two lines TextABCDEFGHIJKLMNOPQRSTUVWXYZ 1234567890 All alphabates")     
  .lineLimit(2, reservesSpace: true)</code></pre>
<!-- /wp:code -->