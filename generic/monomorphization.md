# 단형화 (Monomorphization)

제네릭 코드는 호출부에서 비 제네릭 코드로 전환됩니다:

```rust
fn main() {
    let integer = Some(5);
    let float = Some(5.0);
}
```

위 코드는 아래와 같이 동작합니다

```rust
enum Option_i32 {
    Some(i32),
    None,
}

enum Option_f64 {
    Some(f64),
    None,
}

fn main() {
    let integer = Option_i32::Some(5);
    let float = Option_f64::Some(5.0);
}
```

이것이 바로 비용이 들지 않는 (zero-cost) 추상화 입니다: 러스트의 제네릭은 추상화를 거치지 않고 직접 구체적인 타입을 써서 코딩한 것과 정확히 동일한 결과를 보여줍니다.

단형화는 개별 타잎에 대한 코드를 생성하여 해당 타잎에 대한 코드를 작성한 것과 동일한 코드를 만든다는 뜻입니다.&#x20;
