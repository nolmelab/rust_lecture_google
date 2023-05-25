# 예제 (Example)

`Arc`와 `Mutex`의 동작을 살펴봅시다:

{% code lineNumbers="true" %}
```rust
use std::thread;
// use std::sync::{Arc, Mutex};

fn main() {
    let v = vec![10, 20, 30];
    let handle = thread::spawn(|| {
        v.push(10);
    });
    v.push(1000);

    handle.join().unwrap();
    println!("v: {v:?}");
}
```
{% endcode %}

락을 통해 상호 배제 (Mutal Exclusion)을 하지 않으므로 라인 7과 라인 9 간에 경쟁으로 인해 문제가 발생할 여지가 있다.

```rust
use std::sync::{Arc, Mutex};
use std::thread;

fn main() {
    let v = Arc::new(Mutex::new(vec![10, 20, 30]));

    let v2 = Arc::clone(&v);
    let handle = thread::spawn(move || {
        let mut v2 = v2.lock().unwrap();
        v2.push(10);
    });

    {
        let mut v = v.lock().unwrap();
        v.push(1000);
    }

    handle.join().unwrap();

    println!("v: {v:?}");
}
```

<details>

<summary>발표자 노트</summary>

* `v`는 `Arc`와 `Mutex` 모두에 포함되어 있습니다. 이는 `Arc`와 `Mutex`가 서로 완전히 다른 문제를 위한 도구이기 때문입니다.
  * `Mutex`를 `Arc`로 래핑하는 것은 가변 상태를 스레드들 간에 공유할 때 흔히 사용하는 패턴입니다.
* `v: Arc<_>`를 다른 스레드에서 사용하려면, 먼저 `v2`로 복사를 하고 이를 그 스레드로 이동 해야 합니다. 그래서 람다의 시그니처에 `move`가 있는 것입니다.
* 블록은 `LockGuard`의 범위를 최대한 좁히기 위해 사용되었습니다.

</details>
