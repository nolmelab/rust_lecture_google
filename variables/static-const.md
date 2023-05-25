# 정적 변수(static)와 상수 (const)

프로그램의 글로벌 상태는 결국 정적 변수와 상수로 표현됩니다.

## [상수(`const`)](https://google.github.io/comprehensive-rust/ko/basic-syntax/static-and-const.html#%EC%83%81%EC%88%98const) <a href="#const" id="const"></a>

컴파일 시 값이 정해지는 상수를 선언할 수 있습니다:

```rust
const DIGEST_SIZE: usize = 3;
const ZERO: Option<u8> = Some(42);

fn compute_digest(text: &str) -> [u8; DIGEST_SIZE] {
    let mut digest = [ZERO.unwrap_or(0); DIGEST_SIZE];
    for (idx, &b) in text.as_bytes().iter().enumerate() {
        digest[idx % DIGEST_SIZE] = digest[idx % DIGEST_SIZE].wrapping_add(b);
    }
    digest
}

fn main() {
    let digest = compute_digest("Hello");
    println!("Digest: {digest:?}");
}
```

[Rust RFC Book](https://rust-lang.github.io/rfcs/0246-const-vs-static.html)에 따르면 상수는, 그 상수가 사용되는 곳에 인라인 됩니다.

## [정적변수(`static`)](https://google.github.io/comprehensive-rust/ko/basic-syntax/static-and-const.html#%EC%A0%95%EC%A0%81%EB%B3%80%EC%88%98static) <a href="#static" id="static"></a>

마찬가지로 정적 변수도 선언할 수 있습니다:

```rust
static BANNER: &str = "Welcome to RustOS 3.14";

fn main() {
    println!("{BANNER}");
}
```

[Rust RFC Book](https://rust-lang.github.io/rfcs/0246-const-vs-static.html)에서 언급한 바와 같이, 정적 변수는 별도의 메모리 공간을 가지며, 인라인 되지 않습니다. 정적 변수는 안전하지 않은(unsafe) 러스트와 임베디드 시스템용 코드에서 유용합니다. 이들의 수명은 프로그램이 수행되는 전체 시간과 동일합니다.

가변 정적 데이터에 대해서는 [안전하지 않은 러스트](https://google.github.io/comprehensive-rust/ko/unsafe.html)에서 살펴봅니다.

<details>

<summary>발표자 노트</summary>

* `const`는 C++의 `constexpr`과 매우 비슷합니다.
* 반면에 `static`은 C++의 `const`나 가변 정적 변수와 훨씬 더 유사합니다.
* 프로그램 수행시 그 값이 정해지는 상수가 필요한 경우는 드뭅니다. 그러나 그렇다고 해도, 정적 변수를 사용하는 것 보다는 더 유용하고 안전합니다.

</details>

<details>

<summary>놀미 노트</summary>

* const가 C++의 constexpr과 매우 비슷하다는 건 중요한 내용입니다. 라이브러리 코드를 보면 const 함수가 상당히 많이 있는데 이는 컴파일할 때 계산할 수 있으면 하라는 constexpr의 뜻입니다.

</details>
