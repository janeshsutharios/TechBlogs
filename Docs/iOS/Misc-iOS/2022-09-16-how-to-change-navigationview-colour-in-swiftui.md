---
title: "How to Change NavigationView Colour in SwiftUI"
date: 2022-09-16 09:17:01
categories: ['change navigation title color swiftui', 'change navigationView color swiftui', 'iOS', 'SwiftUI', 'swiftui ios 15 navigation bar color', 'swiftui navigation bar button color']
layout: post
---

<!-- wp:heading {"level":5} -->
<h5><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">iOS 16</mark></h5>
<!-- /wp:heading -->

<!-- wp:image {"id":1421,"width":866,"height":261,"sizeSlug":"full","linkDestination":"none"} -->
<figure class="wp-block-image size-full is-resized">![](/TechBlogs/Assets/Website/2022/09/SwiftUI-Navigation-Color.png)</figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
From iOS 16 we can use <code>.toolbarBackground</code> for the NavigationBar / NavigationView Color. <strong>Don't forget to add </strong><code>.toolbarBackground(.visible, for: .navigationBar)</code>. You can also set title color of Navigation Item by using <code>ToolbarItem</code>


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">struct ContentView : View {
    var body: some View {
        NavigationStack {
            Text("Dashboard")
                .toolbar {
                    ToolbarItem(placement: .principal) {
                        Text("Cool Title")
                            .foregroundColor(.black)
                    }
                }
                .navigationBarTitleDisplayMode(.inline)
                .toolbarBackground(.red, for: .navigationBar)
                .toolbarBackground(.visible, for: .navigationBar)
        }
    }
}</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
<strong><code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">iOS 13 Solution </mark></code></strong>


<!-- /wp:paragraph -->

<!-- wp:media-text {"mediaId":1425,"mediaType":"image"} -->
<div class="wp-block-media-text alignwide is-stacked-on-mobile"><figure class="wp-block-media-text__media">![](/TechBlogs/Assets/Website/2022/09/iOS13-Navigation-Bar-Color-SwiftUI_1-1024x555.png)</figure><div class="wp-block-media-text__content"><!-- wp:paragraph {"placeholder":"Content…"} -->
By setting up the <code>UINavigationBarAppearance</code> we can change the Navigation bar Color. But remember it will affect globally.


<!-- /wp:paragraph --></div></div>
<!-- /wp:media-text -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">struct ContentView: View {    
    init() {
        let navAppearance = UINavigationBarAppearance()
        navAppearance.backgroundColor = .red
        navAppearance.titleTextAttributes = 
        navAppearance.largeTitleTextAttributes = 
        UINavigationBar.appearance().standardAppearance = navAppearance
        UINavigationBar.appearance().scrollEdgeAppearance = navAppearance
    }
    
    var body: some View {
        NavigationView {
            List {
                ForEach((1...50), id: \.self) {
                    Text("Nav Example-- \($0)")
                }
            }
            .navigationBarTitle("NavBar Title")
        }
    }
}</code></pre>
<!-- /wp:code -->