---
title: "Network API call in swift using URLSession"
date: 2022-08-22 13:42:56
categories: ['GET', 'ios', 'iOS', 'POST', 'REST', 'Swift', 'swift', 'WebService']
layout: post
---

<!-- wp:paragraph -->
In this tutorial you will learn about how to fetch data from server or make HTTP Network request using inbuilt Apple’s <code>URLSession</code>, We will use a singleton <code>shared</code> method. You may have a different type of HTTP method like <code>GET POST PUT DELETE</code>. We can use all of them to fetch/update data from Server


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
Let’s jump to the code part 


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
Let's take the <code>GET</code> method  example, so we will be picking up repo JSON from Github URL Inline comments have been added for simplicity.


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
 <code>let urlString = "https://api.github.com/users/janeshsutharios/repos" </code>


<!-- /wp:paragraph -->

<!-- wp:code {"lineNumbers":true} -->
<pre title="" class="wp-block-code"><code lang="swift" class="language-swift line-numbers">    //MARK: Start a Network Task
    func startNetworkTask(urlStr:String, params:, resultHandler: @escaping (Result<Data?, Error>) -> Void)  {
        
        guard let urlObject = URL(string:urlStr) else {
            print("issue in url object")
            resultHandler(.failure(CustomError.urlError))
            return
        }
        // 1: Creating data task
        URLSession.shared.dataTask(with: URLRequest(url: urlObject)) { dataObject, responseObj, errorObject in
            
            if let error = errorObject {
                resultHandler(.failure(error))
            } else {
                resultHandler(.success(dataObject))
            }
        }.resume()
    }
}
// MARK: Model for JSON Data -- For Converting Network Data object into swift readable data object
struct GithubEntity: Codable {
    var id: Int?
    var nodeID, name, fullName: String?
}

// MARK: A custom error enum
enum CustomError: Error {
    case urlError
}
// MARK: use a URL & make api call
let urlString = "https://api.github.com/users/janeshsutharios/repos"
var jsonModel: = 

startNetworkTask(urlStr: urlString, params: ) { result in

  print("recieved data from api-->", result)
    switch result {
   case .success(let dataObject):
       do {
           // 1: updating data to swift Model
           let decoderObject = JSONDecoder()
           jsonModel = try decoderObject.decode(.self, from: dataObject!)
           print("recieved data from codable model -->", jsonModel)
        }
        catch {
           print("error--->", error)
          }
       case .failure(let error):
          print(error.localizedDescription)
      }
}</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
Likewise you can use the same function for POST api, You just need to pass parameters as dictionary 


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
Feel free to add suggestion in comments


<!-- /wp:paragraph -->