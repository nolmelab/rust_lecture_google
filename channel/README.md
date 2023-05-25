# 채널 (Channel)

러스트의 채널은 `Sender<T>` 와 `Receiver<T>` 두 부분으로 구성됩니다. 이 둘은 채널을 통해 서로 연결되어 있지만, 우리는 채널을 볼 수는 없고 이 양 끝단만을 사용하게 됩니다.

```rust
use std::sync::mpsc;
use std::thread;

fn main() {
    let (tx, rx) = mpsc::channel();

    tx.send(10).unwrap();
    tx.send(20).unwrap();

    println!("Received: {:?}", rx.recv());
    println!("Received: {:?}", rx.recv());

    let tx2 = tx.clone();
    tx2.send(30).unwrap();
    println!("Received: {:?}", rx.recv());
}
```

<details>

<summary>발표자 노트</summary>

* `mpsc`는 “Multi-Produce, Single-Consumer”를 의미합니다. `Sender`와 `SyncSender`는 `Clone`을 구현하지만 (즉, 여러개의 producer를 만들수 있습니다) `Receiver`는 `Clone`을 구현하지 않습니다.
* `send()`와 `recv()`는 `Result`를 반환합니다. 만일 `Err`가 반환된다면, 상대방의 `Sender`또는 `Receiver`가 삭제되었고 채널이 닫혔다는 뜻입니다.

</details>
