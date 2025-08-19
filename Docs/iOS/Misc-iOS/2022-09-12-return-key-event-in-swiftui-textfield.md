---
title: "Return Key Event in SwiftUI TextField"
date: 2022-09-12 09:50:54
categories: ['iOS', 'Swift keyboard return key action', 'SwiftUI', 'SwiftUI TextField onChange', 'SwiftUI TextField onSubmit', 'SwiftUI TextField return key action']
layout: post
---

<!-- wp:heading {"level":6} -->
<h6><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">Target iOS 13  </mark></h6>
<!-- /wp:heading -->

<!-- wp:paragraph -->
From the SwiftUI TextField listening events from the return button just use the <code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">onEditingChanged</mark></code> parameter of TextField<br>This is Specially used when someone using TextField For SearchBar in SwiftUI finding solution similar to searchBarSearchButtonClicked where the keyboard dismissed as well.


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">struct ContentView: View {
    
    @State var searchText = ""
    
    var body: some View {
        TextField("Search Bar SwiftUI", text: $searchText, onEditingChanged: { changed in
            if changed {
            }
            else {
                print("User clicked on Return Key")
            }
        })
    }
}</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":6} -->
<h6><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">Solution for iOS 15 onwards :</mark></h6>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">struct ContentView: View {
    @State var searchText = ""
    var body: some View {
        TextField("Search Bar SwiftUI", text: $searchText)
        .onSubmit {
            print("User clicked on return key")
        }
    }
}</code></pre>
<!-- /wp:code -->