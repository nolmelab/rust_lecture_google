# Mutex

[`Mutex<T>`](https://doc.rust-lang.org/std/sync/struct.Mutex.html)를 이용하면 불변 참조를 통해서도 `T`의 값을 수정할 수가 있으며, _이에 더해서_ 한 번에 한 스레드만 `T`의 값을 접근(읽거나 쓰거나)함을 보장해 줍니다:

```rust
use std::sync::Mutex;

fn main() {
    let v = Mutex::new(vec![10, 20, 30]);
    println!("v: {:?}", v.lock().unwrap());

    {
        let mut guard = v.lock().unwrap();
        guard.push(40);
    }

    println!("v: {:?}", v.lock().unwrap());
}
```

모든 `Mutex<T>`는 [`impl<T: Send> Sync for Mutex<T>`](https://doc.rust-lang.org/std/sync/struct.Mutex.html#impl-Sync-for-Mutex%3CT%3E)를 자동으로 구현함을 참조하세요.

<details>

<summary>발표자 노트</summary>

* 러스트의 `Mutex`는 오직 하나의 데이터만 담을 수 있는 컬렉션처럼 볼 수도 있습니다. 다른 컬렉션과 다른 점은, 그 데이터가 동시성 문제로부터 자유롭다는 점입니다.
  * `Mutex`는 뮤텍스를 획득하지 않으면 보호된 데이터에 접근하는 것이 불가능 하도록 디자인 되어 있습니다.
* `&Mutex<T>`에 대해 lock을 획득하면 `&mut T`를 얻을 수 있습니다. `MutexGuard`는 `&mut T`가 획득한 lock보다 오래 살아남지 않음을 보장합니다.
* `Mutex<T>`는 오직 `T`가 `Send`를 구현하는 경우에만 `Send`와 `Sync`를 구현합니다.
* 읽기-쓰기 lock은 `RwLock`을 사용합니다.
* **\[1]** 왜 `lock()`이 `Result`를 반환할까요?
  * `Mutex`를 획득한 스레드에서 패닉이 발생하면, 데이터가 올바르지 않은 상황이 될 수 있습니다. 이를 `Mutex`가 “중독(poisoned)” 되었다고 표현하며, 중독된 뮤텍스에서 `lock()`을 호출하면 실패하고 [`PoisonError`](https://doc.rust-lang.org/std/sync/struct.PoisonError.html)가 발생합니다. 이러한 오류로부터 데이터를 복구하기 위해 `into_inner()`를 호출할 수 있습니다.

**\[1]** 쓰레드가 패닉 상태에 빠져 바로 종료될 경우 정상적인 Drop이나 에러 처리가 누릭될 수 있다. 이럴 경우 어떤 오브젝트들이 비정상적인 상태에 있을 수 있고 이를 음독(Poisoned) 상태라고 한다.

뮤텍스 음독은 락을 잡고 있는 상태에 해당 쓰레드가 패닉한 상태이다. 이렇게 되면 다른 쓰레드들이 락을 잡을 수 없는 상태가 될 수 있다.

로그라켓에서 러스트 관련 좋은 블로그를 올리고 있고 [뮤텍스 음독과 여기에서 복구하는 방법](https://blog.logrocket.com/understanding-handling-rust-mutex-poisoning/) 등을 다루고 있다.



</details>
