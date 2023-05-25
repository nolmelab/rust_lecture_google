# 테스트 모듈 (test module)

단위 테스트는 원래 모듈 밑에 서브 모듈로 만드는 경우가 많습니다. ([플레이그라운드](https://play.rust-lang.org/)에서 다음 테스트를 수행해 보세요):

```rust
fn helper(a: &str, b: &str) -> String {
    format!("{a} {b}")
}

pub fn main() {
    println!("{}", helper("Hello", "World"));
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_helper() {
        assert_eq!(helper("foo", "bar"), "foo bar");
    }
}
```

* 이렇게 서브 모듈로 테스트를 만들면 private한 헬퍼 함수에 대한 단위 테스트도 가능합니다.
* `#[cfg(test)]` 어트리뷰트가 추가된 항목은 `cargo test`를 수행했을 경우에만 동작합니다.

\
