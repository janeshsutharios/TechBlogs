---
title: "How to align Text in SwiftUI?"
date: 2022-09-16 06:50:48
categories: ['iOS', 'SwiftUI', 'swiftui multiline text alignment', 'swiftui text alignment in vstack', 'swiftui text alignment left']
layout: post
---

<!-- wp:media-text {"mediaId":1403,"mediaType":"image"} -->
<div class="wp-block-media-text alignwide is-stacked-on-mobile"><figure class="wp-block-media-text__media">![](/TechBlogs/Assets/Website/2022/09/Text-Alignment-SwiftUI.png)</figure><div class="wp-block-media-text__content"><!-- wp:paragraph {"placeholder":"Content…"} -->
To align Text in iOS Application with <code>.leading .trailing .center</code> of <code>Text</code> use <code><mark>.multilineTextAlignment(.</mark></code>


<!-- /wp:paragraph --></div></div>
<!-- /wp:media-text -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">struct ContentView: View {
    var body: some View {
        Text("A demo long text A demo long textA demo long textA demo long textA demo long textA demo long textA demo long textA demo long textA demo long textA demo long textA demo long text")
            .multilineTextAlignment(.leading)
            .padding(25)
    }
}</code></pre>
<!-- /wp:code -->