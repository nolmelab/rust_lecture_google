# Future

[`Future`](https://doc.rust-lang.org/std/future/trait.Future.html)는 아직 완료되지 않은 연산을 나타내는 객체에 의해 구현되는 트레이트입니다. 미래는 폴링할 수 있으며 폴링은 [`Poll`](https://doc.rust-lang.org/std/task/enum.Poll.html)을 반환합니다.

```rust
use std::pin::Pin;
use std::task::Context;

pub trait Future {
    type Output;
    fn poll(self: Pin<&mut Self>, cx: &mut Context<'_>) -> Poll<Self::Output>;
}

pub enum Poll<T> {
    Ready(T),
    Pending,
}
```

비동기 함수는 impl Future를 반환합니다. 자체 유형에 대해 Future를 구현하는 것도 가능하지만 흔하지는 않습니다. 예를 들어, tokio::spawn에서 반환된 JoinHandle은 Future를 구현하여 조인을 허용합니다.

Future에 적용된 .await 키워드는 해당 Future가 준비될 때까지 현재 비동기 함수를 일시 중지한 다음 해당 출력으로 평가하도록 합니다.

<details>

<summary>발표자 노트</summary>

* Future와  Poll 타잎은 표시된 그대로 구현되어 있으며, 링크를 클릭하면 문서에서 구현된 내용을 볼 수 있습니다.
* 새로운 비동기 프리미티브를 구축하는 대신 비동기 코드 작성에 집중할 것이므로 Pin과 Context에 대해서는 다루지 않고, 간단히 설명하겠습니다:
  * `Context`는 이벤트가 발생할 때 퓨처가 다시 폴링되도록 예약할 수 있도록 합니다.
  * Pin은 퓨처가 메모리에서 이동되지 않도록 하여 해당 퓨처에 대한 포인터가 유효하게 유지되도록 합니다. 이는 .await 이후에도 참조가 유효하게 유지되도록 하는 데 필요합니다.

</details>
