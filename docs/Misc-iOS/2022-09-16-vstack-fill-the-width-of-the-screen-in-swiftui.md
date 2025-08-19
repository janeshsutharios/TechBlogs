---
title: "VStack fill the width of the screen in SwiftUI"
date: 2022-09-16 07:44:05
categories: ['iOS', 'SwiftUI', 'swiftui vstack full width', 'VStack items placement.']
layout: post
---

<!-- wp:paragraph -->
Generally when we use VStack with few views we observed that there is some empty place left over we will see two possible ways- 


<!-- /wp:paragraph -->

<!-- wp:heading {"level":5} -->
<h5>1. By using frame</h5>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">struct ContentView: View {
    var body: some View {
        VStack {
            Text("Nice Post")
            Text("Comment below")
        }
        .frame(
            maxWidth: .infinity,
            maxHeight: .infinity,
            alignment: .topLeading
        )
        .background(Color.red)
    }
}</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":5} -->
<h5>2. Use GeometryReader with frames</h5>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<code>GeometryReader</code> returns a flexible preferred size to its parent layout hence by using arguments geoArgs we can set frame -


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">struct ContentView : View {
    var body: some View {
        GeometryReader { geoArgs in
            VStack {
                Text("Nice Post")
                Text("Comment below")
            }
            .frame(
                width: geoArgs.size.width,
                height: geoArgs.size.height,
                alignment: .topLeading
            )
        }
        .background(Color.red)
    }
}</code></pre>
<!-- /wp:code -->