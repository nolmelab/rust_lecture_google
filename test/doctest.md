# 문서화 주석 테스트 (doctest)

러스트는 문서화주석에 대한 테스트를 내장하여 제공합니다:

````rust
/// Shortens a string to the given length.
///
/// ```
/// use playground::shorten_string;
/// assert_eq!(shorten_string("Hello World", 5), "Hello");
/// assert_eq!(shorten_string("Hello World", 20), "Hello World");
/// ```
pub fn shorten_string(s: &str, length: usize) -> &str {
    &s[..std::cmp::min(length, s.len())]
}
````

* `///` 주석안의 코드 블록은 자동으로 러스트 코드로 인식됩니다.
* 이 코드 블록은 `cargo test` 호출하면 자동으로 컴파일되고 실행됩니다.
* 위 코드를 [Rust Playground](https://play.rust-lang.org/?version=stable\&mode=debug\&edition=2021\&gist=3ce2ad13ea1302f6572cb15cd96becf0)에서 테스트 해 보시기 바랍니다.
