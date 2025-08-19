---
title: "How to hide TabBar/TabView with SwiftUI"
date: 2022-09-04 12:45:05
categories: ['Hide TabBar in swiftUI', 'Hide TabView in swiftUI', 'HideBottomBar when pushed in swiftUI', 'iOS', 'Show navigationBar in swiftUI', 'SwiftUI']
layout: post
---

<!-- wp:image {"id":1353,"sizeSlug":"full","linkDestination":"none"} -->
<figure class="wp-block-image size-full">![](/TechBlogs/Assets/Website/2022/09/Hidebottombarwhenpushed-swiftui.png)</figure>
<!-- /wp:image -->

<!-- wp:heading {"level":5} -->
<h5><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">iOS 16 solution: </mark> .toolbar(.hidden, for: .tabBar)</h5>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">struct ProfileView: View {
  var body: some View {
    Text("ProfileView")
      .toolbar(.hidden, for: .tabBar) /// <-- Hiding the TabBar for a ProfileView.
  }
}</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":5} -->
<h5><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">iOS 13 - iOS 15 Solution: </mark></h5>
<!-- /wp:heading -->

<!-- wp:list {"ordered":true} -->
<ol><li>To hide TabBar when we jumps towards next screen we just have to place NavigationView to the right place. Makesure Embed <code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">TabView</mark></code> inside <code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">NavigationView</mark></code> so creating unique Navigation view for both tabs.</li><li>For setting up navigation title use <code>@State var tabArray </code>with dynamic values.</li></ol>
<!-- /wp:list -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">
import SwiftUI

struct TabBarView: View {
    
    @State var tabSelection: Int = 0
    @State var tabArray = 
    
    var body: some View {
        NavigationView {
            TabView(selection: $tabSelection){
                ForEach(0 ..< tabArray.count, id: \.self) { indexValue in
                    NavigationLink(destination: DetailView()){
                        VStack{
                            Text("\(tabArray) tab -- Click to jump next view")
                        }
                    }
                    .tabItem {
                        Image(systemName: "\(indexValue).circle.fill")
                        Text(tabArray)
                    }
                    .tag(indexValue)
                    
                }
            }
            .navigationBarTitle(tabArray)
        }
    }
}
struct DetailView: View {
    var body: some View {
        Text("Detail View")
            .navigationBarTitle("NavigatedView")
            .navigationBarTitleDisplayMode(.inline)
            .navigationTitle("helllo")
    }
}</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
Thats it :) Complete <a href="https://github.com/janeshsutharios/iOS_Tutorials" target="_blank" rel="noopener">Source code</a> is here 


<!-- /wp:paragraph -->