# async / await

높은 수준에서 비동기 Rust 코드는 "일반적인" 순차 코드와 매우 유사합니다:

```rust
use futures::executor::block_on;

async fn count_to(count: i32) {
    for i in 1..=count {
        println!("Count is: {i}!");
    }
}

async fn async_main(count: i32) {
    count_to(count).await;
}

fn main() {
    block_on(async_main(10));
}
```

<details>

<summary>발표자 노트</summary>

* 이것은 구문을 보여주기 위해 단순화한 예제입니다. 여기에는 장기 실행 연산이나 실제 동시성이 없습니다!
* 비동기 호출의 반환 유형은 무엇인가요?
  * `let future: () = async_main(10);`
* "비동기" 키워드는 구문 설탕입니다. 컴파일러는 반환 유형을 `Future`로 바꿉니다.
* 반환된 Future를 사용하는 방법을 컴파일러에 알려줘야 비동기 `main()`을 만들 수 있습니다.
* 비동기 코드를 실행하려면 실행기(Executor)가 필요합니다. block\_on은 제공된 Future가 완료될 때까지 현재 스레드를 차단합니다.
* .await은 다른 작업이 완료될 때까지 비동기적으로 대기합니다. block\_on과 달리 .await은 현재 스레드를 차단하지 않습니다.
* .await은 비동기 함수(또는 블록) 내에서만 사용할 수 있으며, 나중에 소개합니다.

</details>
