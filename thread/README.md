# 스레드

러스트의 스레드는 다른 언어의 스레드와 유사하게 동작합니다:

```rust
use std::thread;
use std::time::Duration;

fn main() {
    thread::spawn(|| {
        for i in 1..10 {
            println!("Count in thread: {i}!");
            thread::sleep(Duration::from_millis(5));
        }
    });

    for i in 1..5 {
        println!("Main thread: {i}");
        thread::sleep(Duration::from_millis(5));
    }
}
```

* 스레드는 모두 데몬 스레드입니다. 따라서 메인 스레드는 이 스레드들이 끝나기를 기다리지 않습니다.
* 한 스레드에서 발생한 패닉은 다른 스레드에게 영향을 끼치지 않습니다.
  * 패닉은 추가정보(페이로드)를 포함할 수 있으며, 이는 `downcast_ref`로 풀어볼 수 있습니다.

메인 쓰레드가 기다리지 않는다는 것은 그냥 종료시킨다는 뜻입니다.&#x20;

<details>

<summary>발표자 노트</summary>

* 메인 스레드가 자식 스레드를 기다리지 않기 때문에 자식 스레드의 for문은 10까지 가지 않습니다.
* 만약 메인 스레드가 자식 스레드가 끝날 때 까지 기다리기를 원한다면 `let handle = thread::spawn(...)`으로 스레드를 선언한 후 `handle.join()`로 연결하여 사용합니다.
* 자식 스레드에서 발생한 패닉이 메인 스레드에는 영향을 주지 않음을 확인하시기 바랍니다.
* `handle.join()`사용시 `Result` 반환값을 통해 패닉의 추가정보에 접근할 수 있습니다. 이 시점에서 [`Any`](https://doc.rust-lang.org/std/any/index.html)에 대해 이야기를 해 보면 좋습니다.

</details>

