# 범위 쓰레드 (Scoped Threads)

보통, 스레드는 스레드 밖에서 데이터를 빌릴 수 없습니다:

```rust
use std::thread;

fn main() {
    let s = String::from("Hello");

    thread::spawn(|| {
        println!("Length: {}", s.len());
    });
}
```

하지만, [scoped thread](https://doc.rust-lang.org/std/thread/fn.scope.html)에서는 가능합니다:

```rust
use std::thread;

fn main() {
    let s = String::from("Hello");

    thread::scope(|scope| {
        scope.spawn(|| {
            println!("Length: {}", s.len());
        });
    });
}
```

<details>

<summary>발표자 노트</summary>

* `thread::scope` 함수가 완료되면 그 안에서 생성된 모든 스레드들이 종료했음이 보장되기 때문에, 그 때 빌렸던 데이터들을 다시 반환할 수 있기 때문입니다.
* 일반적인 러스트의 빌림 규칙이 적용됩니다: 한 스레드에 의한 가변 빌림 또는 여러 스레드에 대한 불변 빌림중 하나만 가능합니다.

</details>
