# 단위 테스트 (unit test)

단위 테스트는 `#[test]` 로 표시합니다:

```rust
fn first_word(text: &str) -> &str {
    match text.find(' ') {
        Some(idx) => &text[..idx],
        None => &text,
    }
}

#[test]
fn test_empty() {
    assert_eq!(first_word(""), "");
}

#[test]
fn test_single_word() {
    assert_eq!(first_word("Hello"), "Hello");
}

#[test]
fn test_multiple_words() {
    assert_eq!(first_word("Hello World"), "Hello");
}
```

`cargo test` 커맨드를 사용하면 단위 테스트를 찾아서 실행합니다.
