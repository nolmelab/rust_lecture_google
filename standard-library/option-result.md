# Option과 Result

두가지 열거형 타잎인 Option과 Result는 선택적 데이터를 나타냅니다.

```rust
fn main() {
    let numbers = vec![10, 20, 30];
    let first: Option<&i8> = numbers.first();
    println!("first: {first:?}");

    let idx: Result<usize, usize> = numbers.binary_search(&10);
    println!("idx: {idx:?}");
}
```

```rust
/// The `Option` type. See [the module level documentation](self) for more.
#[derive(Copy, PartialEq, PartialOrd, Eq, Ord, Debug, Hash)]
#[rustc_diagnostic_item = "Option"]
#[stable(feature = "rust1", since = "1.0.0")]
pub enum Option<T> {
    /// No value.
    #[lang = "None"]
    #[stable(feature = "rust1", since = "1.0.0")]
    None,
    /// Some value of type `T`.
    #[lang = "Some"]
    #[stable(feature = "rust1", since = "1.0.0")]
    Some(#[stable(feature = "rust1", since = "1.0.0")] T),
}
```

`Option<T>`는 `Some`과 `None`으로 구분되는 열거형입니다.

```rust
#[derive(Copy, PartialEq, PartialOrd, Eq, Ord, Debug, Hash)]
#[must_use = "this `Result` may be an `Err` variant, which should be handled"]
#[rustc_diagnostic_item = "Result"]
#[stable(feature = "rust1", since = "1.0.0")]
pub enum Result<T, E> {
    /// Contains the success value
    #[lang = "Ok"]
    #[stable(feature = "rust1", since = "1.0.0")]
    Ok(#[stable(feature = "rust1", since = "1.0.0")] T),

    /// Contains the error value
    #[lang = "Err"]
    #[stable(feature = "rust1", since = "1.0.0")]
    Err(#[stable(feature = "rust1", since = "1.0.0")] E),
}
```

`Result<T, E>`는 `Ok`와 `Err`로 구분되는 값을 갖는 열거형입니다.

<details>

<summary>발표자 노트</summary>

* `Option`과 `Result`는 표준 라이브러리뿐만아니라 매우 광범위하게 사용되는 타입입니다.
* `Option<&T>` 는 `&T`에 비해 공간 오버헤드가 없습니다.
* `Result`는 오류 처리를 위한 표준 타입입니다. 3일차 과정에서 살펴봅니다.
* `binary_search`는 `Result<usize, usize>`를 반환합니다.
  * 요소가 발견된다면, `Result::Ok`는 발견된 요소의 인덱스를 보유합니다.
  * 아니면, `Result::Err`에는 요소가 삽입되야 하는 인덱스가 포함되어 있습니다.



</details>
