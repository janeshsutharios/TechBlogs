---
title: "How to use datataskPublisher Combine Framework"
date: 2022-08-25 09:59:24
categories: ['Combine with swiftUI', 'iOS', 'SwiftUI', 'webservice call in iOS app']
layout: post
---

<!-- wp:paragraph -->
In this tutorial you will learn about making network call in iOS SwiftUI using Combine Framework & dataTaskPublisher.


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
Combine Framework is mainly used for managing Publisher & Subscriber.  Let me explain in easy way - Subscriber who listens things which Publisher publishes.         In This Tutorial <code>AnyPublisher</code> act as <code>Publisher</code> & <code>Cancellable with .sink</code> act as Subscriber. Note:<strong> Pub & Sub are protocols</strong>  <br>We will be using the Github GET URL <code>"<a href="https://api.github.com/users/janeshsutharios/repos">https://api.github.com/users/janeshsutharios/repos</a>"</code>


<!-- /wp:paragraph -->

<!-- wp:heading {"level":5} -->
<h5>Code for datataskPublisher implementation </h5>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">import Foundation
import Combine

// MARK: Model for JSON Data -- For Converting Network Data object into swift readable data object
struct GithubEntity: Codable {
    var id: Int?
    var nodeID, name, fullName: String?
}

// MARK: Custom Error enum
enum WebServiceError: Error, LocalizedError {
    case unknown, customError(reason: String)
    
    var errorDescription: String? {
        switch self {
        case .unknown:
            return "---Unknown error----"
        case .customError(let reason):
            return reason
        }
    }
}

struct CombileNetworkHelper {
    
    static func fetchFromWebService() -> AnyPublisher<, WebServiceError> {
        // 1: GET Service URL
        let url = URL(string: "https://api.github.com/users/janeshsutharios/repos")!
        
        let urlRequest = URLRequest(url: url)
        
        // 2: Added Publisher
        var dataPublisher: AnyPublisher<, WebServiceError>
        
        // 3: DataTaskPublisher to fetch stream values
        dataPublisher = URLSession.DataTaskPublisher(request: urlRequest, session: .shared)
        
        // 4: tryMap for Creating a closure to map elements with Publisher
            .tryMap { data, response in
                guard let httpResponse = response as? HTTPURLResponse, 200..<300 ~= httpResponse.statusCode else {
                    throw WebServiceError.unknown
                }
                return data
            }
        // 5: Convert Response to Codable mode
            .decode(type: .self, decoder: JSONDecoder())
        // 6: After Recieve data jump to Main Thread so it will be thread safe for UI Activities
            .receive(on: RunLoop.main)
        // 7: mapError is used to map error of custom type with closure
            .mapError { error in
                if let error = error as? WebServiceError {
                    return error
                } else {
                    return WebServiceError.customError(reason: error.localizedDescription)
                }
            }
        // 8:eraseToAnyPublisher is used to expose an instance of AnyPublisher to the downstream subscriber, rather than this publisher’s actual type
            .eraseToAnyPublisher()
        return dataPublisher
    }
}</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
So firstly we created Codable model for Git URL & we have created custom error block as well


<!-- /wp:paragraph -->

<!-- wp:heading {"level":5} -->
<h5>Code Explanation: </h5>
<!-- /wp:heading -->

<!-- wp:paragraph -->
We have DataTaskPublisher with shared session<br><code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-6-color">.tryMap</mark></code> is used for Creating a closure to map elements with Publisher, here we are transforming data.<br><code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-6-color">.decode(..</mark> </code>Mapping the <code>response</code> to codable type i.e. <code>GithubEntity</code><br><code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-6-color">.receive(on:</mark></code> After Recieve data jump to Main Thread so it will be thread safe for UI Activities < Just like <code>DisatchQueue.main.async></code> <br><code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-6-color">.mapError</mark> i</code>s used to map error of custom type with closure in our case it's <code>enum WebServiceError</code><br><code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-6-color">.eraseToAnyPublisher</mark></code> is used to expose an instance of AnyPublisher to the downstream subscriber, rather than this publisher’s actual type So here we are mapping to<code> , WebServiceError</code>


<!-- /wp:paragraph -->

<!-- wp:heading {"level":5} -->
<h5><code>ContentView:<mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-6-color"> </mark></code>where we are invoking network call - </h5>
<!-- /wp:heading -->

<!-- wp:paragraph -->
Here we will use .sink subscriber which listen values from the Publisher<code> AnyPublisher<, WebServiceError></code><br>On <code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-6-color">.sink(.. </mark></code> we have  two parameters one is <code>completion</code> & another is receive value which is <code>closure type </code>


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">
struct ContentView: View {
    
    @State var apiDataSubscriber: Cancellable? = nil
    
    func hitWebService() {
        apiDataSubscriber = CombileNetworkHelper.fetchFromWebService().sink(receiveCompletion: { completion in
            switch completion {
            case .finished:
                break
            case .failure(let error):
                print(error.localizedDescription)
            }
        }, receiveValue: { response in
            print("\n Response Recieved-->", response)
        })
    }
    
    var body: some View {
        Button(
            action: { hitWebService() },
            label: { Text("Click Me").font(.subheadline) }
        )
    }
}</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
Now launch the application & click the button the response will get printed. :)<br>The Xcode project file can be <a href="https://github.com/janeshsutharios/iOS_Tutorials/tree/main/Combine_Example_SwiftUI" title="">download from here </a><br>Hope the article was easy to understand.. Thanks.<br>That's all :)


<!-- /wp:paragraph -->