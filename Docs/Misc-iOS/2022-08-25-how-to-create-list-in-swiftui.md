---
title: "How to create list in SwiftUI"
date: 2022-08-25 06:35:41
categories: ['Create TableView in swiftUI', 'iOS', 'iOS ListView', 'List in swiftUI', 'Similar to List View in Android', 'SwiftUI', 'swiftUI scrollable items']
layout: post
---

<!-- wp:paragraph -->
Just like a UITableView in UIKit It’s List in SwiftUI which is useful for creating the ListView in iOS Application.


<!-- /wp:paragraph -->

<!-- wp:image {"id":1233,"width":454,"height":338,"sizeSlug":"full","linkDestination":"none"} -->
<figure class="wp-block-image size-full is-resized">![](/TechBlogs/Assets/Website/2022/08/SwiftUI-List.png)</figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
In This Tutorial we will be discussing about three type of List Creation in SwiftUI


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
1.Creating static list in SwiftUI 


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
2. Create List with dynamic type 


<!-- /wp:paragraph -->

<!-- wp:heading {"level":5} -->
<h5>1. Creating static list in SwiftUI</h5>
<!-- /wp:heading -->

<!-- wp:paragraph -->
List { is type of struct in SwiftUI so let’s add


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">List {
    Text("iOS")
    Text("Android")
}</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
That's all :)


<!-- /wp:paragraph -->

<!-- wp:heading {"level":5} -->
<h5>2. Now Let’s create List with dynamic type in SwiftUI</h5>
<!-- /wp:heading -->

<!-- wp:paragraph -->
Step 1: Create a Data Object who conforms to Identifiable protocol which is required for unique identity 


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">struct DeviceList: Identifiable {
    let id:Int
    let name: String
}</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
Step 2: Create @State var with list of object, this also could be the objects from webservice


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">@State var itemArray = [DeviceList(id: 1, name: "iPhone 6"),
                        DeviceList(id: 2, name: "iPhone 7"),
                        DeviceList(id: 3, name: "iPhone X")]</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
Step 3: Add it to the list by using of ForEach 


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">List {
    ForEach(itemArray) { itemObject in
        Text(itemObject.name)
    }
}</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
The Final code look like


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">struct ContentView: View {
    @State var itemArray = [DeviceList(id: 1, name: "iPhone 6"),
                            DeviceList(id: 2, name: "iPhone 7"),
                            DeviceList(id: 3, name: "iPhone X")]
    
    var subscriber: Cancellable? = nil
    
    var body: some View {
        NavigationView {
            // MARK:  Static List
            //            List {
            //                Text("iOS")
            //                Text("Android")
            //            }
            // MARK:  Dynamic List
            List {
                ForEach(itemArray) { itemObject in
                    Text(itemObject.name)
                }
            }
            .navigationTitle("List in SwiftUI")
        }
        
    }
}</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
You can also use <code>ForEach</code> with range like 


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">List {
     ForEach((1...130), id: \.self) {
       Text("Index---> \($0)")
     }
}</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
Download Code Example for <a href="https://github.com/janeshsutharios/iOS_Tutorials/tree/main/SideBar_SwiftUI" target="_blank" rel="noopener">SwiftUI here</a>  - 


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
That's all :)


<!-- /wp:paragraph -->