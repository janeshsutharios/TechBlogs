---
title: "How to Create Complex UI with SwiftUI"
date: 2022-08-29 11:44:00
categories: ['components in swiftui', 'composing-complex-interfaces', 'iOS', 'SwiftUI']
layout: post
---

<!-- wp:image {"id":1323,"sizeSlug":"full","linkDestination":"none"} -->
<figure class="wp-block-image size-full">![](/TechBlogs/Assets/Website/2022/08/Ecom-SwiftUI-app-1.png)</figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
In this tutorial we will create a mini SwiftUI App with complex interference. We will cover following modules by creating mini E-commerce SwiftUI Application, Here all <code>SFSymbol</code> icons are used so It's lightweight and no external image dependencies :) 


<!-- /wp:paragraph -->

<!-- wp:list {"ordered":true} -->
<ol><li>A <mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">NavigationBar</mark> in SwiftUI with custom title colour</li><li><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">SearchBar</mark> in swiftUI</li><li><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">Pager</mark> in SwiftUI with page-control buttons</li><li>Fix height <mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">list</mark> in swiftUI</li><li><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">Grid</mark> in SwiftUI with customisation </li></ol>
<!-- /wp:list -->

<!-- wp:paragraph -->
Let's jump to the code - 


<!-- /wp:paragraph -->

<!-- wp:heading {"level":5} -->
<h5><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">1. Create SearchBar in SwiftUI -</mark></h5>
<!-- /wp:heading -->

<!-- wp:list {"ordered":true} -->
<ol><li>Use <code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">TextField</mark></code> with <code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">.overlay(</mark></code> of search icon</li><li>We have used <code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">HStack</mark></code> here because SearchTextField Cross icon and Cancel button all are aligned horizontally </li><li><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color"><code>isEditingMode</code></mark> is used to know weather to searchBar is Active ? if so show up cancel button.</li><li>This is UI Only code as in this article we are focusing on building UI with many components.  <br>A precise code would be --></li></ol>
<!-- /wp:list -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">import SwiftUI

struct SearchBarView: View {
    
    @State private var isEditingMode = false
    @Binding var currentSearchText: String
 
    var body: some View {
        HStack {
 
            TextField("Search Products Here ..", text: $currentSearchText)
                .padding(8)
                .padding(.horizontal, 26)
                .background(Color(.systemGray6))
                .cornerRadius(8)
                .overlay(
                    HStack {
                        Image(systemName: "magnifyingglass")
                            .foregroundColor(.gray)
                            .frame(minWidth: 0, maxWidth: .infinity, alignment: .leading)
                            .padding(.leading, 7)

                        if isEditingMode {
                            Button(action: {
                                self.currentSearchText = ""
                            }) {
                                Image(systemName: "multiply.circle.fill")
                                    .foregroundColor(.gray)
                                    .padding(.trailing, 7)
                            }
                        }
                    }
                )
                .padding(.horizontal, 9)
                .onTapGesture {
                    self.isEditingMode = true
                }
 
            if isEditingMode {
                Button(action: {
                    self.isEditingMode = false
                    self.currentSearchText = ""
 
                }) {
                    Text("Cancel")
                }
                .padding(.trailing, 9)
                .animation(.easeOut)
            }
        }
    }
}

struct SearchBarView_Previews: PreviewProvider {
    static var previews: some View {
        SearchBarView(currentSearchText: .constant(""))
        
    }
}</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":5} -->
<h5><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">2. Creating Pager in SwiftUI</mark></h5>
<!-- /wp:heading -->

<!-- wp:list {"ordered":true} -->
<ol><li><code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">TabView</mark></code> is used to create pager in SwiftUI clip shape for customisation <code>clipShape(RoundedRectangle(cornerRadius: 10.0, style: .continuous))</code></li><li><code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">setupAppearanceForPager()</mark></code> is used for changing colour of the Pager dots which invokes on <code>.onAppear</code> method</li><li>Select <code>TabView</code> Style<mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">  <code>.tabViewStyle(PageTabViewStyle())</code></mark> this settings is for pager<br> code for pager ---></li></ol>
<!-- /wp:list -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">import SwiftUI

struct PageView: View {
    var body: some View {
        TabView {
            ForEach(0..<2) { i in
                ZStack {
                    Color.white
                    VStack {
                        HStack() {
                            Image(systemName: "laptopcomputer")
                                .resizable()
                                .aspectRatio(contentMode: .fit)
                                .frame(height: 70)
                                .foregroundColor(.pink)
                            VStack(alignment: .leading, spacing: 0) {
                                // Spacer()
                                Text("Macbook Exclusive Offer")
                                    .padding(.leading,10)
                                    .foregroundColor(.black)
                                HStack{
                                    Text("$1000")
                                        .strikethrough(true, color: .black)
                                        .padding(.leading,10).font(.caption)
                                    Text ("$700")
                                        .font(Font.headline.weight(.semibold))
                                    Text ("30% off")
                                        .font(Font.body.weight(.light))
                                        .foregroundColor(.green)
                                    
                                }
                                .foregroundColor(.black)
                                //Spacer()
                                .frame(height: 50)
                            }
                        }
                        Divider()
                        Text("Get 5% instant Cashback up to ₹6,000 with qualifying credit cards. Terms apply. The all-new MacBook Air")
                            .font(.system(size: 10))
                    }
                    
                }
                .clipShape(RoundedRectangle(cornerRadius: 10.0, style: .continuous))                
            }
            .padding(, 10)
        }
        .frame(maxHeight: .infinity)
        .frame(width: UIScreen.main.bounds.width)
        .tabViewStyle(PageTabViewStyle())
        .background(Color.red)
        .onAppear {
            setupAppearanceForPager()
        }
    }
    
    func setupAppearanceForPager() {
        UIPageControl.appearance().currentPageIndicatorTintColor = .black
        UIPageControl.appearance().pageIndicatorTintColor = UIColor.black.withAlphaComponent(0.2)
    }
}

struct PageView_Previews: PreviewProvider {
    static var previews: some View {
        PageView()
    }
}</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":5} -->
<h5><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">3. Creating Custom List in SwiftUI</mark></h5>
<!-- /wp:heading -->

<!-- wp:list {"ordered":true} -->
<ol><li>Create <code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">DeviceEntity</mark></code> model for dataSet of List or TableView</li><li>Since we have items in horizontally use List with <code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">HStack</mark></code> </li><li><code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">.listStyle(.plain)</mark></code> used for remove padding from the List rows</li><li>To setup image in list with custom height <code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">resizable</mark></code> used with <code>aspectRatio</code> to <code>.fit </code></li><li><code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">strikethrough</mark></code> used to make a Old & New price label </li></ol>
<!-- /wp:list -->

<!-- wp:paragraph -->
Code for ListView -->


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">import SwiftUI

struct DeviceEntity:Identifiable {
    let id = UUID()
    var name: String
}
struct ProductListView: View {
    
    @State var deviceList: = [DeviceEntity(name: "iPhone 15 Exclusive Offer"),
                                            DeviceEntity(name: "iPhone 14 Exclusive Offer")]
    
    
    var body: some View {
        List(deviceList) { currentObject in
            HStack {
                Image(systemName: "iphone")
                    .resizable()
                    .aspectRatio(contentMode: .fit)
                    .frame(height: 50, alignment: .center)
                    .foregroundColor(.pink)
                
                VStack(alignment: .leading, spacing: 0) {
                    // Spacer()
                    Text(currentObject.name)
                        .padding(.leading,10)
                    HStack{
                        Text("$1000")
                            .strikethrough(true, color: .black)
                            .padding(.leading,10).font(.caption)
                        Text ("$700")
                            .font(Font.headline.weight(.semibold))
                        Text ("30% off")
                            .font(Font.body.weight(.light))
                            .foregroundColor(.green)
                        
                    }
                    //Spacer()
                    .frame(height: 50)
                }//.environment(\.defaultMinListRowHeight, 100)
            }
        }
        .listStyle(.plain)
        .frame(height:170)
    }
}

struct ProductListView_Previews: PreviewProvider {
    static var previews: some View {
        ProductListView()
    }
}</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":5} -->
<h5><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">4. Create Custom Grid in SwiftUI</mark></h5>
<!-- /wp:heading -->

<!-- wp:list {"ordered":true} -->
<ol><li>Here we are creating Grid or <mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">collectionview</mark> in swiftUI by using <code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">LazyHGrid</mark></code> </li><li><code>itemsRangeForGrid</code> defines how many item required for the Grid, in our current example we are creating Grid of 4 items </li><li><code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">GridItem</mark></code> for item configuration   </li><li>As in our example we have set of two items vertically we will be using <code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">VStack</mark></code> & add Images & Text there</li><li><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color"><code>.overlay</code>( i</mark>s used to create BorderRadius  with colour </li></ol>
<!-- /wp:list -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">import SwiftUI

struct CustomGridLayout: View {
    let itemsRangeForGrid = 1...4
    let gridRows = [
        GridItem(spacing:5),
        GridItem(spacing: 5),
    ]
    
    let gridItemWidth = (UIScreen.main.bounds.width-30)/2
    
    var body: some View {
        ScrollView(.horizontal) {
            
            LazyHGrid(rows: gridRows, alignment: .center,spacing: 5) {
                
                ForEach(itemsRangeForGrid, id: \.self) { item in
                    
                    ZStack {
                        VStack(alignment: .center, spacing: 5) {
                            Image(systemName: "tshirt")
                                .resizable()
                                .aspectRatio(contentMode: .fit)
                                .frame(height: 75, alignment: .center)
                                .foregroundColor(.pink)
                            
                                Text("Men Tshirts")
                                    .frame(maxWidth: .infinity, alignment: .center)
                                    .font(.system(size: 20))
                                Text("Grab Now")
                                    .frame(maxWidth: .infinity, alignment: .center)
                                    .foregroundColor(.green)
                                    .font(.system(size: 10))
                            
                        }.frame(width: gridItemWidth, height:145, alignment: .center)
                            .overlay(
                                RoundedRectangle(cornerRadius: 10)
                                    .stroke(Color.red, lineWidth: 1)
                            )
                    }
                }
            }
            .frame(height: 300)
        }
        .padding(,10)
    }
}

struct GridLayout_Previews: PreviewProvider {
    static var previews: some View {
        CustomGridLayout()
    }
}</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":5} -->
<h5><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">5. Dashboard file where we link all SwiftUI View</mark></h5>
<!-- /wp:heading -->

<!-- wp:list {"ordered":true} -->
<ol><li><code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">NavigationView</mark></code> is used for creating Navigation in SwiftUI & We will Embed all item to ScrollView so that user can scroll over items<br>Since we have long vertical list we are using <code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">VStack</mark></code> </li><li>Use .<code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">toolbar</mark></code> for setting u <code>navigationBar</code> title & Text</li><li><code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color"> .navigationBarTitleDisplayMode(.inline)</mark></code> For shorter <code>navigationBar</code> </li></ol>
<!-- /wp:list -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">import SwiftUI

struct ContentView: View {
    
    @State var searchBarText:String = ""
    
    var body: some View {
        
        NavigationView {
            
            ScrollView {
                VStack(alignment: .leading) {
                    SearchBarView(currentSearchText: $searchBarText)
                    
                    LazyHStack {
                        PageView()
                    }
                    .padding(, 0)
                    .background(Color.blue)
                    .frame(height:175)
                    
                    Text("Top Deals Of The Day 🌟🌟🌟")
                        .multilineTextAlignment(.leading)
                        .padding(.all, 10)
                        .font(.headline)
                    
                    ProductListView()
                    
                    CustomGridLayout()
                    
                    //Spacer()
                }
                .toolbar {
                    ToolbarItem(placement: .principal) {
                        VStack {
                            Text("🛒Ecom Application").font(.headline)
                            Text("Buy products👕").font(.subheadline)
                        }
                        .foregroundColor(.red)
                    }
                }
            }
            .navigationBarTitleDisplayMode(.inline)
        }
        
    }
}

struct Dashboard_Previews: PreviewProvider {
    static var previews: some View {
        ContentView()
    }
}</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
That's all :)


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
Complete Source code<a href="https://github.com/janeshsutharios/iOS_Tutorials/tree/main/SwiftUI_LayoutBuilding" target="_blank" rel="noopener" title=""> available here </a>


<!-- /wp:paragraph -->