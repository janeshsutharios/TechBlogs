---
title: "Change background color of view in SwiftUI"
date: 2022-09-16 07:22:56
categories: ['iOS', 'SwiftUI', 'swiftui background color full screen', 'swiftui change background color programmatically', 'swiftui empty view with background color']
layout: post
---

<!-- wp:paragraph -->
Here we can Use <code>ZStack</code> to set the background of the view. Basically <code>ZStack</code> adding up the elements Top on it. or we can say as on Z-Axis. Here we can use<code> Color.red </code>which is bit similar to emptyView hence all other items will be added on the <strong>Z-Axis </strong>


<!-- /wp:paragraph -->

<!-- wp:heading {"level":5} -->
<h5>1. Background Color inside safeArea</h5>
<!-- /wp:heading -->

<!-- wp:image {"id":1409,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large">![](/TechBlogs/Assets/Website/2022/09/change-background-color-swiftUI-1-1-1024x497.png)</figure>
<!-- /wp:image -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">struct ContentView: View {
    var body: some View {
        ZStack {
            Color.red
        }
    }
}</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":5} -->
<h5>1. Background Color cover all screen</h5>
<!-- /wp:heading -->

<!-- wp:image {"id":1410,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large">![](/TechBlogs/Assets/Website/2022/09/change-background-color-swiftUI-2-1-1024x510.png)</figure>
<!-- /wp:image -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">struct ContentView: View {
    var body: some View {
        ZStack {
            Color.red
                .ignoresSafeArea()
            Text("Thanks for Posting ")
            
        }
    }
}</code></pre>
<!-- /wp:code -->