# From과 Into

타입은 용이한 형변환을 위해 [`From`](https://doc.rust-lang.org/std/convert/trait.From.html)과 [`Into`](https://doc.rust-lang.org/std/convert/trait.Into.html)를 구현합니다:

```rust
fn main() {
    let s = String::from("hello");
    let addr = std::net::Ipv4Addr::from([127, 0, 0, 1]);
    let one = i16::from(true);
    let bigger = i32::from(123i16);
    println!("{s}, {addr}, {one}, {bigger}");
}
```

[`From`](https://doc.rust-lang.org/std/convert/trait.From.html)이 구현되면 [`Into`](https://doc.rust-lang.org/std/convert/trait.Into.html) 역시 자동으로 구현됩니다:

```rust
fn main() {
    let s: String = "hello".into();
    let addr: std::net::Ipv4Addr = [127, 0, 0, 1].into();
    let one: i16 = true.into();
    let bigger: i32 = 123i16.into();
    println!("{s}, {addr}, {one}, {bigger}");
}
```

아래는 convert 모듈에 구현된 제네릭 Into입니다. From 구현이 있는 모든 타잎에 대해 동작합니다.&#x20;

```rust
impl<T, U> const Into<U> for T
where
    U: ~const From<T>,
{
    /// Calls `U::from(self)`.
    ///
    /// That is, this conversion is whatever the implementation of
    /// <code>[From]&lt;T&gt; for U</code> chooses to do.
    fn into(self) -> U {
        U::from(self)
    }
}
```

<details>

<summary>발표자 노트</summary>

* 그렇기 때문에 사용자 정의 타입의 경우에도 `From` 만 구현하는 것이 일반적입니다.
* “`String`으로 변환할 수 있는 모든 것“과 같은 함수의 인수 타입을 선언할 때에는 `Into`를 사용해야 함을 조심하세요. 그래야만, 함수는 `From`을 구현한 타입과 `Into` _만_ 구현한 타입 모두를 인자로 받을 수 있습니다.

</details>
