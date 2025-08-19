---
title: "How to create TabView in SwiftUI"
date: 2022-08-30 12:20:22
categories: ['Create UIPager in SwiftUI', 'Customise TabView in swiftUI', 'iOS', 'SwiftUI', 'TabView example in SwiftUIcarousel swiftui']
layout: post
---

<!-- wp:image {"id":1331,"sizeSlug":"full","linkDestination":"none"} -->
<figure class="wp-block-image size-full">![](/TechBlogs/Assets/Website/2022/08/UIPager-In-SwiftUI-TabView.png)</figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
Just Like a <code>UIPager</code> in Swift, we will use <code>TabView</code> in SwiftUI to create a page effect with dot indicator on it.


<!-- /wp:paragraph -->

<!-- wp:list {"ordered":true} -->
<ol><li><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color"><code>TabView</code></mark> switches between multiple childviews So we can swipe around and it will jump to the next item.</li><li>Here we will be using the <code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">ForEach</mark></code> which is used to add multiple items over it.</li><li><code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">ZStack</mark></code> is used for just a background effect.</li><li><code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">.tabViewStyle(.page)</mark></code> is used to create dot indicator pager effect </li><li>Optional -<mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color"> <code>indexViewStyle(.page(backgroundDisplayMode: .never))</code></mark> when we use never it will create no background effect as shown in reference image 1.If we use <mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color"><code>.always </code></mark>it will show a background around the pager. You can try <mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color"><code>.interactive</code></mark> and play around. :)<br></li></ol>
<!-- /wp:list -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">import SwiftUI
struct ContentView: View {
    var body: some View {
        VStack {
            PagerInSwiftUI()
            Spacer()
        }
    }
}

struct PagerInSwiftUI: View {
    var body: some View {
        TabView {
            ForEach(0..<5) { i in
                ZStack {
                    Color.red
                    Text("Current Page -> \(i)").foregroundColor(.white)
                }.clipShape(RoundedRectangle(cornerRadius: 10.0, style: .continuous))
                    .frame(height:200)
            }
            .padding(.all, 10)
        }
        .frame(width: UIScreen.main.bounds.width, height: 200)
        .tabViewStyle(.page)
        .indexViewStyle(.page(backgroundDisplayMode: .never))// To set indexStyle(Background of pager)
    }
}

struct ContentView_Previews: PreviewProvider {
    static var previews: some View {
        ContentView()
    }
}</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
A more example to embed into complex UI is here - <a href="https://janeshswift.com/ios/swiftui/how-to-create-complex-ui-with-swiftui/" target="_blank" rel="noopener">https://janeshswift.com/ios/swiftui/how-to-create-complex-ui-with-swiftui/</a>


<!-- /wp:paragraph -->