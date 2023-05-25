# 구조체 분해 (역구조화)

```rust
struct Foo {
    x: (u32, u32),
    y: u32,
}

#[rustfmt::skip]
fn main() {
    let foo = Foo { x: (1, 2), y: 3 };
    match foo {
        Foo { x: (1, b), y } => println!("x.0 = 1, b = {b}, y = {y}"),
        Foo { y: 2, x: i }   => println!("y = 2, x = {i:?}"),
        Foo { y, .. }        => println!("y = {y}, other fields were ignored"),
    }
}
```

<details>

<summary>발표자 노트</summary>

* Foo의 리터럴 값을 다른 패턴과 일치하도록 변경합니다.&#x20;
* Foo에 새 필드를 추가하고 필요에 따라 패턴을 변경합니다.&#x20;
* 캡처와 상수 표현식을 구분하기 어려울 수 있습니다. 두 번째 가지(팔)의 2를 변수로 변경하고 미묘하게 작동하지 않는지 확인해 보세요. 상수로 변경하고 다시 작동하는 것을 확인합니다.

`..`으로 여러 필드를 생략할 수 있습니다.&#x20;

</details>

<details>

<summary>놀미 노트</summary>

구조체 분해나 열거형 분해 모두 let, if let, while let 구문에서도 사용할 수 있습니다. 참조나 \&mut 참조로도 분해 가능한지 실험해 볼 수 있겠습니다.

</details>
