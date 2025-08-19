---
title: "How to create CheckBox in SwiftUI"
date: 2022-09-02 12:48:05
categories: ['iOS', 'List with Checkboxes in SwiftUI', 'Multiple Selection in SwiftUI', 'Selecting multiple rows in swiftUI', 'SwiftUI']
layout: post
---

<!-- wp:media-text {"mediaId":1340,"mediaType":"image","mediaWidth":40,"mediaSizeSlug":"medium"} -->
<div class="wp-block-media-text alignwide is-stacked-on-mobile" style="grid-template-columns:40% auto"><figure class="wp-block-media-text__media">![](/TechBlogs/Assets/Website/2022/09/CheckBox-List-SwiftUI-153x300.png)</figure><div class="wp-block-media-text__content"><!-- wp:list {"ordered":true} -->
<ol><li>Here we gonna create a List In SwiftUI with checkboxes in row items, where user can select Multiple checkboxes And the data is managed through <code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">ObservedObject</mark></code></li><li> There is a <code>Button</code> Called "Get Selected Values" on click of it,  it will fetch the selected row of the list & print it on debugger </li><li>In this example we will be using Mock data for dataSets, In your case you can use RealDatasets from WebServer</li></ol>
<!-- /wp:list -->

<!-- wp:paragraph -->
Let's start with code -


<!-- /wp:paragraph --></div></div>
<!-- /wp:media-text -->

<!-- wp:paragraph -->
-


<!-- /wp:paragraph -->

<!-- wp:heading {"level":5} -->
<h5>1. Create a Json File for Mock Data</h5>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<code>Xcode->New->File->Strings. </code>Rename it to<code> Movies.json</code>


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">[
    {
        "title": "Bajrangi Bhaijaan",
    },
    {
        "title": "Kuch Kuch Hota he",
    },
    {
        "title": "Americal PIE",
    },
    {
        "title": "Hang over Part 3",
    },
    {
        "title": "Edge of Tomorrow",
    },
    {
        "title": "Blade Runner 2049",
    },
    {
        "title": "Inception",
    },
    {
        "title": "The Matrix",
    }
]</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":5} -->
<h5>2. Add MovieEntity.swift for Model</h5>
<!-- /wp:heading -->

<!-- wp:paragraph -->
Create a struct which conforms to codable & holds dataSets of JSON file


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">struct MovieEntity {
    let title: String
    var isFavorite = false
}

extension MovieEntity: Decodable {
    enum CodingKeys: String, CodingKey {
        case title
    }
}
</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
We will be using <code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">ObservableObject</mark></code> which can be used as dataSource for the List


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">class MoviesModel: ObservableObject {
    @Published var data:  = 
    init() {
        self.data = MockDataJSON.movies
    }
}</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":5} -->
<h5>3. Create .swift file MockDataJSON.swift</h5>
<!-- /wp:heading -->

<!-- wp:paragraph -->
We will be reading the data from Json & feed into the <code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">MovieEntity</mark></code> with use of <code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">JSONDecoder</mark></code>


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">import Foundation
struct MockDataJSON {
    static var movies:  = {
        let url = Bundle.main.url(forResource: "Movies", withExtension: "json")!
        let data = try! Data(contentsOf: url)
        let decoder = JSONDecoder()
        return try! decoder.decode(.self, from: data)
    }()
}</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":5} -->
<h5>4. CheckBox class creation</h5>
<!-- /wp:heading -->

<!-- wp:paragraph -->
Create a  checkbox class which has Image <code>Image(systemName: isChecked ? "checkmark.square.fill" : "square")</code> So based on <code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">isChecked</mark></code> we are selected Checkbox image.


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">import SwiftUI

struct CheckBoxView: View {
    
    let isChecked: Bool;
    
    var body: some View {
        Image(systemName: isChecked ? "checkmark.square.fill" : "square")
            .foregroundColor(isChecked ? Color(UIColor.systemBlue) : Color.secondary)
    }
}

struct CheckBoxView_Previews: PreviewProvider {
    static var previews: some View {
        Group {
            CheckBoxView(isChecked: true)
            CheckBoxView(isChecked: false)
        }
        .padding()
        .previewLayout(.sizeThatFits)
    }
}</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":5} -->
<h5>5.Set up the cell of List</h5>
<!-- /wp:heading -->

<!-- wp:paragraph -->
Create a file named ListItemCell.swift which contains the row item of List. It contains the CheckBox & title 


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">import SwiftUI

struct ListItemCell: View {
    
    @ObservedObject var movie:MoviesModel
    var currentIndex:Int = 0
    var body: some View {
        HStack {
            Button(action: { self.movie.data.isFavorite.toggle() }) {
                CheckBoxView(isFilled: movie.data.isFavorite)
            }
            Text(movie.data.title)
            Spacer()
        }
    }
}

struct ListItemCell_Previews: PreviewProvider {
    static var previews: some View {
        ListItemCell(movie: MoviesModel())
            .padding()
            .previewLayout(.sizeThatFits)
    }
}</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":5} -->
<h5>6. Create MoviesListView.swift which contains ListView</h5>
<!-- /wp:heading -->

<!-- wp:paragraph -->
Use <code>VStack</code> where we about to place <code>List</code> & <code>Button</code> & use of StateObject so we can listen the <code>@published </code>values, Here we have used <code>enumerated()</code> on Array type because we required <code>index</code> of array


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">import SwiftUI

struct MoviesListView: View {
    @StateObject var movies = MoviesModel()
    var body: some View {
        VStack {
            List {
                ForEach(Array(movies.data.enumerated()), id: \.offset) { index, element in
                    ListItemCell(movie: movies, currentIndex: index)
                }
            }
            Button {
                print("Selected values ----->", movies.data.filter{$0.isFavorite})
            } label: {
                Text("Get Selected Values")
            }
        }
        .navigationBarTitle("All Movies")
    }
}

struct MoviesView_Previews: PreviewProvider {
    static var previews: some View {
        NavigationView {
            MoviesListView()
        }
    }
}
// Note: Pass data as --@State var movies:  = MockDataJSON.movies</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
Final <a href="https://github.com/janeshsutharios/iOS_Tutorials/tree/main/Checkbox-SwiftUI" target="_blank" rel="noopener">code is here </a>


<!-- /wp:paragraph -->