# Arc

[`Arc<T>`](https://doc.rust-lang.org/std/sync/struct.Arc.html) allows shared read-only access via `Arc::clone`:

```rust
use std::thread;
use std::sync::Arc;

fn main() {
    let v = Arc::new(vec![10, 20, 30]);
    let mut handles = Vec::new();
    for _ in 1..5 {
        let v = Arc::clone(&v);
        handles.push(thread::spawn(move || {
            let thread_id = thread::current().id();
            println!("{thread_id:?}: {v:?}");
        }));
    }

    handles.into_iter().for_each(|h| h.join().unwrap());
    println!("v: {v:?}");
}
```

<details>

<summary>발표자 노트</summary>

* `Arc`는 “Atomic Reference Counted“를 의미하며, 스레드 안정성을 보장하는 `Rc`라고 생각하면 됩니다.
* `T`가 `Clone`을 구현하든 안하든 `Arc<T>`는 `Clone`을 구현합니다. `Send`와 `Sync`는 `T`가 이들을 구현하는 경우에만 구현됩니다.
* `Arc::clone()`는 아토믹 연산을 수행하기 때문에 그 때 코스트가 좀 있지만, 일단 `clone()`이 끝난 후 `T`를 사용하는 대에는 아무런 오버헤드가 없습니다.
* 순환 참조가 발생하지 않도록 주의해야 합니다. 러스트는 순환 참조를 감지하는 가비지 컬랙터가 없습니다.
  * 순환 참조를 피하는데 `std::sync::Weak`가 도움이 될 것입니다.

</details>
