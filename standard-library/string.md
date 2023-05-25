# String 문자열

[`String`](https://doc.rust-lang.org/std/string/struct.String.html)은 힙에 할당되고 가변 길이의 표준 UTF-8 문자열 버퍼입니다:

```rust
fn main() {
    let mut s1 = String::new();
    s1.push_str("Hello");
    println!("s1: len = {}, capacity = {}", s1.len(), s1.capacity());

    let mut s2 = String::with_capacity(s1.len() + 1);
    s2.push_str(&s1);
    s2.push('!');
    println!("s2: len = {}, capacity = {}", s2.len(), s2.capacity());

    let s3 = String::from("🇨🇭");
    println!("s3: len = {}, number of chars = {}", s3.len(),
             s3.chars().count());
}
```

`String`은 [`Deref<Target = str>`](https://doc.rust-lang.org/std/string/struct.String.html#deref-methods-str)을 구현합니다. 이는 , `String` 값에 대해서도 `str`의 모든 메서드를 호출 할 수 있다는 의미 입니다.

Deref는 코딩을 편하게 하는 중요한 수단입니다. [러스트 언어 문서의 Deref 설명](https://rinthel.github.io/rust-lang-book-ko/ch15-02-deref.html)을 참고하세요.

<details>

<summary>발표자 노트</summary>

* String::new는 새 빈 문자열을 반환하며, 문자열에 푸시할 데이터의 양을 알고 있는 경우 String::with\_capacity를 사용합니다.
* String::len은 문자열의 크기를 바이트 단위로 반환합니다(문자 단위의 길이와 다를 수 있음).
* String::chars는 실제 문자에 대한 이터레이터를 반환합니다. 문자는[ 자소 클러스터](https://exploringjs.com/impatient-js/ch\_unicode.html)로 인해 사람이 "문자"로 간주하는 것과 다를 수 있습니다.
* 사람들이 문자열을 언급할 때 \&str 또는 String에 대해 이야기할 수 있습니다.
* 유형이 `Deref<Target = T>`를 구현하면 컴파일러는 T에서 메서드를 투명하게 호출할 수 있게 해줍니다.
  * `String`은 `str`의 메서드에 투명하게 액세스할 수 있는 `Deref<Target = str>`을 구현합니다.
  * &#x20;let s3 = s1.deref(); 및 let s3 = &\*s1; 을 작성하여 비교해 보세요.
* 문자열은 바이트 벡터를 감싸는 래퍼로 구현되며, 벡터에서 지원되는 많은 연산이 문자열에서도 지원되지만 몇 가지 추가 보증이 있습니다.
* 문자열을 색인화하는 여러 가지 방법을 비교합니다:
  * `s3.chars().nth(i).unwrap()` 여기서 i는 캐릭터 경계 내부 또는 외부일 수 있습니다.
  * `s3[0..4]`, 여기서 슬라이스는 캐릭터 경계가 아닐 수 있습니다.



</details>
