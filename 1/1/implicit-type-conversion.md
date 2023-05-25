# 묵시적 형변환 (Implicit Type Conversion)

러스트는 [C++ 와 다르게](https://en.cppreference.com/w/cpp/language/implicit\_conversion) 타입 간 _묵시적 변환_을 자동으로 적용하지 않습니다. 아래 예시를 확인해 보세요:

```rust
fn multiply(x: i16, y: i16) -> i16 {
    x * y
}

fn main() {
    let x: i8 = 15;
    let y: i16 = 1000;

    println!("{x} * {y} = {}", multiply(x, y));
}
```

러스트의 정수형 타입은 모두 [`From<T>`](https://doc.rust-lang.org/std/convert/trait.From.html) 와 [`Into<T>`](https://doc.rust-lang.org/std/convert/trait.Into.html) 트레이트를 구현하고 있으며, 이를 통해 타입 변환이 이루어 집니다. `From<T>` 트레이트는 `from()` 메서드를 가지고 있고, `Into<T>`트레잇은 `into()` 메서드를 가지고 있습니다. 러스트에서는 `From`과 `Into` 트레잇을 구현함으로써, 타입 간 변환이 가능하다는 것을 표현합니다.

표준 라이브러리에는 `From<i8> for i16`가 구현되어 있는데 이것은 `i8` 타입의 변수 `x`를 `i16::from(x)`를 호출하여 `i16`타입으로 변환할 수 있다는 의미입니다. 혹은 더 간단하게 `x.into()`를 사용할 수도 있습니다. 이것이 가능한 이유는 `From<i8> for i16` 구현을 가지고 있으면 `Into<i16> for i8` 구현이 자동으로 생성되기 때문입니다.

이는 사용자 정의 타입에도 동일하게 적용되는 규칙입니다. 따라서 `From`만을 구현해도 `Into`까지 자동으로 구현이 됩니다.

1. 위 예제코드를 실행하고 어떤 컴파일 에러가 발생하는지 확인해 보세요.
2. `into()`를 사용하여 코드를 수정하세요.
3. `x`와 `y`를 `f32`이나 `bool`, `i128` 등으로 바꿔서 해당 타입들로 변환이 되는지 확인해보세요. 작은 사이즈 타입에서 큰 사이즈로 변경해보시고 그 반대로도 해보세요. [표준 라이브러리 문서](https://doc.rust-lang.org/std/convert/trait.From.html)에서 시도해 본 케이스가 구현되어 있는지 확인해 보세요.

<details>

<summary>놀미 노트</summary>

* 트레이트는 3일차에서 자세히 다루는데 여기서는 C#이나 Java의 인터페이스와 거의 같다고 보면 됩니다. 처음 트레이트를 봤을 때 C#의 인터페이스와 같다고 생각했고, 실제로도 그렇습니다.
* From 트레이트를 구현하면 Into는 자동으로 제네릭 구현으로 적용됩니다. 이와 같이 러스트는 작게 잘 개념화된 트레이트의 힘으로 코드를 구조화합니다.

</details>
