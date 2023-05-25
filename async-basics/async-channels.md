# Async Channels

몇몇 크레이트는 async/await 기능을 지원합니다. 예를 들어 토키오 채널이 있습니다:

```rust
use tokio::sync::mpsc::{self, Receiver};

async fn ping_handler(mut input: Receiver<()>) {
    let mut count: usize = 0;

    while let Some(_) = input.recv().await {
        count += 1;
        println!("Received {count} pings so far.");
    }

    println!("ping_handler complete");
}

#[tokio::main]
async fn main() {
    let (sender, receiver) = mpsc::channel(32);
    let ping_handler_task = tokio::spawn(ping_handler(receiver));
    for i in 0..10 {
        sender.send(()).await.expect("Failed to send ping.");
        println!("Sent {} pings so far.", i + 1);
    }

    std::mem::drop(sender);
    ping_handler_task.await.expect("Something went wrong in ping handler task.");
}
```

<details>

<summary>발표자 노트</summary>

* 채널 크기를 3으로 변경하고 실행에 어떤 영향을 미치는지 확인합니다.
* 전반적으로 인터페이스는 오전 수업에서 본 동기화 채널과 비슷합니다.
* std::mem::drop 호출을 제거해 보세요. 어떻게 되나요? 왜 그럴까요?
* Flume crate에는 동기 및 비동기 송수신을 모두 구현하는 채널이 있습니다. 이는 IO와 CPU 처리 작업이 모두 많은 복잡한 애플리케이션에 유용할 수 있습니다.
* 비동기 채널로 작업하는 것이 더 나은 이유는 다른 Future와 결합하여 복잡한 제어 흐름을 만들 수 있기 때문입니다.

</details>
