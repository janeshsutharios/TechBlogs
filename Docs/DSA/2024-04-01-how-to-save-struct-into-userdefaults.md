---
title: "How to save struct into UserDefaults ?"
date: 2024-04-01 05:20:58
categories: ['Swift']
layout: post
---

<!-- wp:paragraph -->
<code>NSUserDefaults</code>, which is now called <code>UserDefaults</code> in Swift, is a mechanism for storing small pieces of data persistently across app launches. It's typically used for storing user preferences, settings, and other simple data.


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
The reason why <code>UserDefaults</code> can only store class instances and not other types directly is due to its design. <code>UserDefaults</code> is primarily intended for storing property list types, which include basic data types such as strings, numbers, booleans, dates, arrays, and dictionaries. These types are automatically bridged to their Foundation equivalents (e.g., <code>String</code> to <code>NSString</code>, <code>Int</code> to <code>NSNumber</code>, etc.).


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
Class instances, when stored in <code>UserDefaults</code>, are archived into data representations using <code>NSCoding</code>, a protocol that allows objects to be encoded and decoded for storage and retrieval. By conforming to <code>NSCoding</code>, a class can provide methods to convert its properties to and from a binary data representation, allowing it to be stored in <code>UserDefaults</code>.


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
However, primitive types like structs or enums do not conform to <code>NSCoding</code> by default, so they cannot be stored directly in <code>UserDefaults</code>. If you want to store a struct or enum in <code>UserDefaults</code>, you would need to encode and decode it yourself into a property list compatible type (e.g., as an array or dictionary of primitive types) before storing it.


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">//--- Saving struct into Userdefaults --//

struct Person: Codable {
    var name: String
    var age: Int
}

let person = Person(name: "John", age: 30)

let encoder = JSONEncoder()
if let encoded = try? encoder.encode(person) {
    UserDefaults.standard.set(encoded, forKey: "person")
}

if let savedPersonData = UserDefaults.standard.data(forKey: "person"),
    let savedPerson = try? JSONDecoder().decode(Person.self, from: savedPersonData) {
    print(savedPerson) // This will print: Person(name: "John", age: 30)
}
// --In this example, the Person struct conforms to Codable, which implicitly conforms to NSCoding. We encode the person struct using JSONEncoder and store the resulting data in UserDefaults. Later, we decode the data back into a Person struct using JSONDecoder.---//</code></pre>
<!-- /wp:code -->