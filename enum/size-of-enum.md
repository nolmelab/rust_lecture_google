# 열거형 타잎의 크기

러스트의 열거형은 정렬(alignment)로 인한 제약을 고려하여 크기를 잘  맞춰서(tight 하게) 잡습니다:

{% code lineNumbers="true" %}
```rust
use std::mem::{align_of, size_of};

macro_rules! dbg_size {
    ($t:ty) => {
        println!("{}: size {} bytes, align: {} bytes",
                 stringify!($t), size_of::<$t>(), align_of::<$t>());
    };
}

enum Foo {
    A,
    B,
}

fn main() {
    dbg_size!(Foo);
}
```
{% endcode %}

구글 교육 문서는 자세한 설명 없이 새로운 기능을 도입하여 찾아볼 수 있도록 안내하는 방법을 많이 쓰고 있습니다. 구조체, 트레이트, 반복자 등이 모두 그런 예였습니다.&#x20;

여기서는 매크로를 예시를 통해 사용예를 보여주고 이를 통해 편리하게 매크로를 사용하는 방법을 알려줍니다.&#x20;

<details>

<summary>발표자 노트</summary>

* 러스트는 열거형 variant를 구분하기 위해 내부적으로 식별자(discriminant) 필드를 사용합니다.
*   C와의 연동과 같은 이유로 식별자를 직접 지정할 수도 있습니다:

    ```rust
    #[repr(u32)]
    enum Bar {
        A,  // 0
        B = 10000,
        C,  // 10001
    }

    fn main() {
        println!("A: {}", Bar::A as u32);
        println!("B: {}", Bar::B as u32);
        println!("C: {}", Bar::C as u32);
    }
    ```

    `repr` 속성이 없다면 10001이 2 바이트로 표현가능하기 때문에 식별자의 타입 크기는 2 바이트가 됩니다.
* 다른 타입들도 확인해보세요.
  * `dbg_size!(bool)`: size 1 bytes, align: 1 bytes
  * `dbg_size!(Option<bool>)`: size 1 bytes, align: 1 bytes (니치 최적화, 아래 설명 참조)
  * `dbg_size!(&i32)`: size 8 bytes, align: 8 bytes (64비트 머신인 경우)
  * `dbg_size!(Option<&i32>)`: size 8 bytes, align: 8 bytes (널포인터 최적화, 아래 설명 참조)
* \[1] 니쉬(niche, 틈) 최적화: 러스트는 열거형 식별자를 사용되지 않은 비트 패턴과 병합합니다.

</details>

<details>

<summary>놀미 노트</summary>

\[1] 니쉬 최적화는 열거형이 분류의 구분을 하기위해 추가로 필요한 필드를 최적화하는 기법을 말합니다. `Option` 열거형이 `Option<bool>`에 대해 1바이트만 필요합니다. 구분자 필드는 어디로 갔을까요? 어떻게 Some(false)와 None을 구분할까요? 이와 같은 질문에 얼마나 깊게 살피고 답해야 할까요?&#x20;

</details>
