# 📖 Strong vs Weak References in Swift (ARC Explained)

Swift uses **Automatic Reference Counting (ARC)** to manage memory.
Every time you create a new object (class instance), ARC keeps track of how many **strong references** point to it.

When no strong references remain → the object is automatically **deallocated**.

---

## 🔒 Strong References

By default, all references in Swift are **strong**.
That means they **own** the object and increase its reference count.

```swift
class Student {
    var marks: Int
    init(marks: Int) {
        self.marks = marks
        print("Student created with marks: \(marks)")
    }
    deinit {
        print("Student deallocated")
    }
}

func strongExample() {
    var student1: Student? = Student(marks: 95)
    var student2 = student1 // strong reference
    
    print("Student1:", student1)
    print("Student2:", student2)
    
    student1 = nil // reference count decreases but still 1 left
    print("After nil student1:", student2)
    
    student2 = nil // now ref count = 0 → object is deallocated
}
```

### Output:

```
Student created with marks: 95
Student1: Optional(Student)
Student2: Optional(Student)
After nil student1: Optional(Student)
Student deallocated
```

✅ Object stayed alive until **all strong references** were removed.

---

## 🪶 Weak References

A **weak** reference does **not** increase the reference count.
It just “points” to the object while someone else owns it.
If the last strong reference is removed, the object is deallocated, and the weak reference is automatically set to `nil`.

```swift
func weakExample() {
    weak var weakStudent: Student? // weak reference
    
    do {
        let newStudent = Student(marks: 50)
        weakStudent = newStudent
        print("Inside scope:", weakStudent)
    }
    
    // newStudent goes out of scope → last strong reference gone
    print("After scope:", weakStudent) // nil
}
```

### Output:

```
Student created with marks: 50
Inside scope: Optional(Student)
Student deallocated
After scope: nil
```

✅ Object deallocated as soon as the strong reference was gone.
✅ Weak reference automatically set to `nil`.

---

## ⚖️ Strong vs Weak Summary

| Feature                                              | Strong Reference | Weak Reference                         |
| ---------------------------------------------------- | ---------------- | -------------------------------------- |
| Increases reference count?                           | ✅ Yes            | ❌ No                                   |
| Keeps object alive?                                  | ✅ Yes            | ❌ No                                   |
| Automatically becomes `nil` when object deallocates? | ❌ No             | ✅ Yes                                  |
| Use case                                             | Normal ownership | Avoiding retain cycles, optional links |

---

## 🚀 Practical Usage

* Use **strong** when you want to own an object.
* Use **weak** when:

  * You want to avoid **retain cycles** (e.g., delegates).
  * You don’t want to keep the object alive unnecessarily.
  * You just need a temporary, optional link.

---

## 📌 Retain Cycle Example (Why Weak Matters)

```swift
class Teacher {
    var student: Student?
}

class Student {
    var teacher: Teacher?
}
```

Both `Teacher` and `Student` strongly reference each other → retain cycle → memory leak.

✅ Fix: make one side `weak` (usually the delegate or child).

```swift
class Student {
    weak var teacher: Teacher?
}
```

---

💡 **Rule of Thumb**:
👉 Use **strong** by default.
👉 Use **weak** when you want a reference that does not keep the object alive (delegates, parent-child, caches).

