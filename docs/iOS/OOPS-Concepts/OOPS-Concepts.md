## 1. Classes and Objects
A class is a blueprint for creating objects that encapsulate data and behavior. An object is an instance of a class, representing a specific entity with its own values and functionality. This approach helps organize code in a modular, reusable, and scalable way.

```swift
class Student {
    var name: String
    var age: Int
    var grade: String

    init(name: String, age: Int, grade: String) {
        self.name = name
        self.age = age
        self.grade = grade
    }

    func displayInfo() {
        print("Name: \(name), Age: \(age), Grade: \(grade)")
    }
}

// Usage -
let student1 = Student(name: "Aarav", age: 14, grade: "8th")
student1.displayInfo()
````
