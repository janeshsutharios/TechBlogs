---
title: "How to Hide Home Indicator In SwiftUI ?"
date: 2022-09-13 06:13:39
categories: ['hide home button iphone', 'hide home indicator swiftui', 'iOS', 'ios home indicator', 'prefershomeindicatorautohidden', 'SwiftUI']
layout: post
---

<!-- wp:heading {"level":6} -->
<h6><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">iOS 16 Solution</mark></h6>
<!-- /wp:heading -->

<!-- wp:image {"id":1380,"width":867,"height":388,"sizeSlug":"full","linkDestination":"none"} -->
<figure class="wp-block-image size-full is-resized">![](/TechBlogs/Assets/Website/2022/09/Hide-Home-Indicator-SwiftUI.png)</figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
To Hide Bottom home indicator line on SwiftUI use <mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color"><code> .persistentSystemOverlays(.hidden)</code></mark>. It also support animation. First it will show dark & turns to light gray with animation. 


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">struct ContentView: View {
    var body: some View {
        Text("iPhone Home Indicator is Hidden👇🏽")
            .persistentSystemOverlays(.hidden)
    }
}</code></pre>
<!-- /wp:code -->