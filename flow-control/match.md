# match 표현식

match 키워드는 하나 이상의 패턴에 대해 값을 일치시키는 데 사용됩니다. 그런 의미에서 일련의 if let 표현식처럼 작동합니다:

```rust
fn main() {
    match std::env::args().next().as_deref() {
        Some("cat") => println!("Will do cat things"),
        Some("ls")  => println!("Will ls some files"),
        Some("mv")  => println!("Let's move some files"),
        Some("rm")  => println!("Uh, dangerous!"),
        None        => println!("Hmm, no program name?"),
        _           => println!("Unknown program name!"),
    }
}
```

`if let`과 마찬가지로 매치의 모든 팔(arm)은 같은 타입이어야 합니다. 팔이 블록이라면 블록의 마지막 표현식이 그 타입이 됩니다. 위의 예제에서 매치 표현식의 타입은 `()`입니다.

<details>

<summary>발표자 노트</summary>

* `match` 표현식을 변수에 할당하고 그 값을 출력해보세요.
* **`[1]`**` ``.as_deref()`를 지워보고, 이 때 나오는 에러를 설명해주세요.
  * `std::env::args().next()`는 `Option<String>` 값을 반환하는데, `String`은 직접 매치할 수 없습니다.
  * `as_deref()`는 `Option<T>`를 `Option<&T::Target>`으로 바꿔줍니다. 이 경우는 `Option<String>`에서 `Option<&str>`로 바뀝니다.
  * 이제는 패턴 매칭으로 `Option` 안의 `&str`을 매치할 수 있습니다.

match 보다 as\_deref()가 더 난이도가 높습니다.

아래는 \&Option\<T>에서 Option<\&T::Target>으로 변환하는 as\_deref() 함수와 as\_ref() 함수입니다.

<pre class="language-rust"><code class="lang-rust"><strong>#[stable(feature = "option_deref", since = "1.40.0")]
</strong>#[rustc_const_unstable(feature = "const_option_ext", issue = "91930")]
pub const fn as_deref(&#x26;self) -> Option&#x3C;&#x26;T::Target>
where
    T: ~const Deref,
{
    match self.as_ref() {
    // T는 Deref를 구현합니다. T::Target 타잎을 얻습니다.
    // String의 deref 구현은 &#x26;str을 돌려줍니다.
        Some(t) => Some(t.deref()),
        None => None,
    }
}
</code></pre>

```rust
#[inline]
#[rustc_const_stable(feature = "const_option_basics", since = "1.48.0")]
#[stable(feature = "rust1", since = "1.0.0")]
pub const fn as_ref(&self) -> Option<&T> {
    match *self {
        // 매칭되면 x는 &T 타잎입니다.
        Some(ref x) => Some(x), 
        None => None,
    }
}
```

러스트는 위와 같이 작은 트레이트로 구성됩니다. 트레이트가 많지만 일관된 패턴이 있으므로 계속 보면 익숙해집니다. 대신 꽤 오랜 시간 봐야 합니다.

[러스트 언어 문서의 Deref 설명](https://rinthel.github.io/rust-lang-book-ko/ch15-02-deref.html)을 참고하세요.

</details>

