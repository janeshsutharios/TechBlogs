---
title: "How to create Navigation in SwiftUI ?"
date: 2022-09-12 12:06:50
categories: ['iOS', 'iOS 16 onwards Navigation', 'SwiftUI', 'swiftui navigation link', 'swiftui navigation programmatically', 'SwiftUI NavigationView']
layout: post
---

<!-- wp:heading {"level":6} -->
<h6><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">iOS 16 onwards</mark></h6>
<!-- /wp:heading -->

<!-- wp:image {"id":1376,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large">![](/TechBlogs/Assets/Website/2022/09/NavigationView-SwiftUI-1024x538.png)</figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
User <code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">NavigationStack</mark></code>  for top Header(NavView) & use <code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">NavigationLink</mark></code> for jump to next view -


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">struct NavigationViewExample: View {
    var body: some View {
        NavigationStack {
            VStack {
                NavigationLink {
                    Text("Click Here")
                } label: {
                    Text("Detail View")
                }
            }
            .navigationTitle("Navigation iOS 16")
        }
    }
}</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
Additionally you can use<code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color"> .navigationBarTitleDisplayMode(.inline)</mark></code> for lesser height NavigationBar


<!-- /wp:paragraph -->

<!-- wp:heading {"level":5} -->
<h5><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">Use Of .navigationDestination</mark></h5>
<!-- /wp:heading -->

<!-- wp:paragraph -->
To jump with specific value use <code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">navigationDestination</mark></code> let me  explain you in simple way by giving Genuine example -<br>Create a <code>Hashable</code> model in Swift - where  <code>hash(into </code>is used for Hashable conformance &  <code> static func == (lhs</code> is for Equatable protocol & <code>countryName</code> is property 


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">class CountryModel: Hashable, Equatable {
    
    static func == (lhs: CountryModel, rhs: CountryModel) -> Bool {
        lhs.countryName == rhs.countryName
    }
    
    func hash(into hasher: inout Hasher) {
        hasher.combine(countryName)
    }
    
    var countryName: String = ""
    
    init(title: String) {
        self.countryName = title
    }
}</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
Now we can use <code>navigationDestination</code> with CountryModel which is Hashable -


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">struct NavigationViewExample: View {
    let countryList: 
    var body: some View {
        
        NavigationStack {
            VStack(spacing: 30) {
                
               NavigationLink {
                    DetailView()
                } label: {
                    Text("A Simple Navigation")
                }
                
                NavigationLink(value: CountryModel.init(title: "India")) {
                    Text("Jump To India")
                }
                
                NavigationLink(value: CountryModel.init(title: "USA")) {
                    Text("Jump To USA")
                }
                
            }
            .navigationDestination(for: CountryModel.self, destination: { currentStuff in
                Text("Successfully entered in -> " + currentStuff.countryName)
            })
            
            .navigationTitle("Navigation Demo")
        }
    }
}

struct DetailView :View {
    
    var body: some View {
        Text("This is Detail View")
    }
}</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
Any suggestion ?  comments are welcomed 👇🏽👇🏽👇🏽


<!-- /wp:paragraph -->