# Actor vs Class vs Struct in Swift

| Aspect | **Struct** | **Class** | **Actor** |
|---|---|---|---|
| **Type semantics** | Value type (copied on assignment) | Reference type (shared instance) | Reference type (shared instance) |
| **Inheritance** | ❌ No | ✅ Single inheritance | ❌ No (only `NSObject` for ObjC interop) |
| **Protocol conformance** | ✅ Yes | ✅ Yes | ✅ Yes, but sync protocol requirements need `nonisolated` or isolated conformance |
| **Identity (`===`)** | ❌ No | ✅ Yes | ✅ Yes |
| **Mutating methods** | Need the `mutating` keyword | Not needed | Not needed, since mutation is isolated |
| **`let` instance behavior** | Fully immutable | Properties can still be mutated | Properties mutable only from inside the actor |
| **Memberwise init** | ✅ Auto-generated | ❌ Must write `init` | ❌ Must write `init` |
| **`deinit`** | ❌ No (except `~Copyable` structs) | ✅ Yes | ✅ Yes (isolated `deinit` in Swift 6.2+) |
| **Memory** | Usually stack/inline (heap if boxed, escaping, or existential) | Heap, ARC-managed | Heap, ARC-managed |
| **Copy-on-write** | Built-in for stdlib collections, manual for custom | N/A | N/A |
| **Thread safety** | Safe by copy, since each thread gets its own copy | ❌ Not safe, needs locks or queues manually | ✅ Safe, with compiler-enforced data isolation |
| **`Sendable`** | Implicit if all stored properties are `Sendable` (non-public types) | Only if `final` with immutable `Sendable` props, otherwise `@unchecked Sendable` | ✅ Always implicitly `Sendable` |
| **External access** | Synchronous | Synchronous | `await` required from outside the actor (async hop) |
| **Reentrancy** | N/A | N/A | ⚠️ Reentrant at every `await`, so state can change across suspension points |
| **`nonisolated` members** | N/A | N/A | ✅ For sync access to immutable or `Sendable` state |
| **Global actor support** | Can be annotated (`@MainActor struct`) | Can be annotated (`@MainActor class`) | Is itself an actor; `@globalActor` defines shared ones |
| **ObjC interop** | ❌ No | ✅ Via `NSObject` / `@objc` | Limited |
| **Performance** | Fastest, with no ARC or indirection for simple types | ARC overhead, dynamic dispatch unless `final` | ARC plus executor hop cost for each `await` |
| **Typical use** | Models, DTOs, config, value data | Shared mutable state, UIKit, delegates, ObjC APIs | Shared mutable state across concurrent tasks |

### Quick rule of thumb

1. **Start with a struct.** Use it when the data has no identity and copying is fine.
2. **Use a class** when you need identity, inheritance, ObjC/UIKit interop, or synchronous access to shared state. Make it `final`, and use a lock for thread safety.
3. **Use an actor** when shared mutable state is accessed from multiple concurrent tasks and async access is acceptable.

### Actor vs lock-based `final class`

This choice is relevant to your `StateBroadcaster` work. An actor forces `await` on every call and brings reentrancy concerns. A `final class` with `OSAllocatedUnfairLock` marked `@unchecked Sendable` gives you **synchronous** access. That is often better inside `NEPacketTunnelProvider` callbacks, or when sync protocol requirements must be satisfied. The trade-off is that correctness is then your responsibility instead of the compiler's.
