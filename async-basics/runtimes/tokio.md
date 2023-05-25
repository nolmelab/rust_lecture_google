# Tokio

토키오는 다음을제공합니다:

* 비동기 코드 실행을 위한 멀티 스레드 런타임.&#x20;
* 표준 라이브러리의 비동기 버전.&#x20;
* 대규모 라이브러리 환경&#x20;

```rust
use tokio::time;

async fn count_to(count: i32) {
    for i in 1..=count {
        println!("Count in task: {i}!");
        time::sleep(time::Duration::from_millis(5)).await;
    }
}

#[tokio::main]
async fn main() {
    tokio::spawn(count_to(10));

    for i in 1..5 {
        println!("Main task: {i}");
        time::sleep(time::Duration::from_millis(5)).await;
    }
}
```

<details>

<summary>발표자 노트</summary>

* 이제 tokio::main 매크로를 사용하여 메인 함수를 비동기로 만들 수 있습니다.
* `spawn` 함수는 새로운 동시 실행 "Task"를 만듭니다.
* 참고: spawn은 Future를 사용하므로 count\_to에서 .await을 호출하지 않습니다.
* count\_to가 (보통) 10이 되지 않는 이유는 무엇인가요? 이것은 비동기 취소의 예입니다. tokio::spawn은 완료될 때까지 기다릴 수 있는 핸들을 반환합니다.
* 스폰 대신 count\_to(10).await을 사용해 보세요.
* tokio::spawn에서 반환된 작업을 기다려 보세요.

스포일러이지만 코드를 보는 게 나을 듯 해서 적습니다.&#x20;

```rust
#[tokio::main]
async fn main() {
    let task = tokio::spawn(count_to(10));

    for i in 1..5 {
        println!("Main task: {i}");
        time::sleep(time::Duration::from_millis(5)).await;
    }

    // JoinHandle을 대기
    let result = task.await;
    if let Err(e) = result {
      println!("error: {:?}", e);
    }
}
```

</details>
