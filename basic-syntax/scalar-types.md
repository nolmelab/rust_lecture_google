# 스칼라 타잎 (Scalar Types)

| Signed integers        | `i8`, `i16`, `i32`, `i64`, `i128`, `isize` | `-10`, `0`, `1_000`, `123i64` |
| ---------------------- | ------------------------------------------ | ----------------------------- |
| Unsigned integers      | `u8`, `u16`, `u32`, `u64`, `u128`, `usize` | `0`, `123`, `10u16`           |
| Floating point numbers | `f32`, `f64`                               | `3.14`, `-10.0e20`, `2f32`    |
| Strings                | `&str`                                     | `"foo"`, `"two\nlines"`       |
| Unicode scalar values  | `char`                                     | `'a'`, `'α'`, `'∞'`           |
| Booleans               | `bool`                                     | `true`, `false`               |

각 타입의 크기는 다음과 같습니다:

* 정수(`i`) 및 부동소수형(`f`)은 뒤의 숫자와 같은 비트 수 입니다. (`i8` = 8비트)
* `isize` 와 `usize` 는 포인터와 같은 크기입니다.
  * _역주: 32 비트 시스템에서는 32 비트, 64 비트 시스템에서는 64 비트. C의 `int`와 같음._
* `char` 32 비트 입니다.
* `bool`은 8 비트 입니다.

<details>

<summary>발표자 노트</summary>

* 원시 문자열을 사용하면 이스케이프가 비활성화된 \&str 값을 만들 수 있습니다(r"\n" == "\n"). 따옴표 양쪽에 같은 수의 #를 사용하여 큰따옴표를 삽입할 수 있습니다:

```rust
fn main() {
    println!(r#"<a href="link.html">link</a>"#);
    println!("<a href=\"link.html\">link</a>");
}
```

* 바이트 문자열을 사용하면 &\[u8] 값을 직접 만들 수 있습니다

```rust
fn main() {
    println!("{:?}", b"abc");
    println!("{:?}", &[97, 98, 99]);
}
```

</details>

<details>

<summary>연습</summary>

* [\[Rust By Example : Primitives\]](https://doc.rust-lang.org/rust-by-example/primitives.html)를 카고로 만든 프로젝트에서 vscode나 IDE에서 직접 실행해 봅니다.

</details>
