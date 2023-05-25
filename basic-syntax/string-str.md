# String과 str

이제 러스트의 두 가지 문자열 타입에 대해서 이해해 보겠습니다:

```rust
fn main() {
    let s1: &str = "World";
    println!("s1: {s1}");

    let mut s2: String = String::from("Hello ");
    println!("s2: {s2}");
    s2.push_str(s1);
    println!("s2: {s2}");
    
    let s3: &str = &s2[6..];
    println!("s3: {s3}");
}
```

러스트 용어:

* `&str`은 문자열 슬라이스에 대한 (불변) 참조입니다.
* `String`은 문자열을 담을 수 있는 버퍼입니다.

<details>

<summary>발표자 노트</summary>

* `&str`은 문자열 슬라이스의 불변 참조입니다. 러스트에서 문자열은 UTF-8로 인코딩된 데이터를 의미합니다. 문자열 리터럴(`"Hello"`)은 프로그램 바이너리에 저장됩니다.
* 러스트의 `String`타입은 실제로는 문자열을 이루는 바이트에 대한 백터(`Vec<u8>`)입니다. `Vec<T>`가 `T`를 소유하고 있듯이, `String`이 가리키고 있는 문자열은 `String`의 소유입니다.
* 다른 많은 타입들처럼 `String::from`는 문자열 리터럴로부터 문자열을 생성합니다. `String::new()`는 새로운 빈 문자열을 생성합니다. `push()`와 `push_str()`메서드를 사용하여 문자열 데이터를 추가 할 수 있습니다.
* `format!()` 매크로는 변수의 값을 문자열로 변환하는 편리한 방법입니다. 이 매크로는 `println!()` 매크로와 동일한 포맷팅 형식을 지원합니다.
* `&`와 범위 연산자를 이용하여 `String`에서 `&str`슬라이스를 빌려올 수 있습니다.
* 당신이 C++ 프로그래머 라면: `&str`는 C++의 `const char*`와 유사하지만 항상 유효한 문자열을 가리킨다는 점이 다릅니다. 러스트의 `String`은 C++의 `std::string` 과 대략 거의 동일합니다. (주요 차이점: 러스트의 `String`은 UTF-8 인코딩 바이트만 포함할 수 있으며 작은 문자열 최적화(small-string optimization)는 사용하지 않습니다.

</details>

<details>

<summary>놀미 노트</summary>

* String과 \&str, fs 모듈을 사용하여 문자열 다루는 연습을 많이 해보면 처음 러스트를 배울 때 많은 도움이 됩니다.

</details>

<details>

<summary>연습</summary>

* [Rust by example의 문자열 연습](https://doc.rust-lang.org/rust-by-example/std/str.html)입니다.&#x20;
* [Rust lang book의 문자열 설명](https://doc.rust-lang.org/book/ch08-02-strings.html)의 코드 내용을 따라서 해봅니다.

</details>
