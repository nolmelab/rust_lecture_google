# 문자열 (String and Iterator)

이번 훈련은 웹 서버의 라우팅 컴포넌트를 구현합니다. 서버는 _요청 경로(request path)_ 를 처리할 수 있는 여러 개의 _경로 접두사(path prefix)_ 로 구성됩니다. 경로 접두사는 와일드카드문자를 포함할 수 있습니다. 아래 단위 테스트 코드를 참조하세요.

아래 코드를 [https://play.rust-lang.org/](https://play.rust-lang.org/)에 복사하고 테스트를 통과해 보시기 바랍니다. 중간 결과값을 `Vec`에 할당하지 않도록 주의 하시기 바랍니다:

```rust
// TODO: remove this when you're done with your implementation.
#![allow(unused_variables, dead_code)]

pub fn prefix_matches(prefix: &str, request_path: &str) -> bool {
    unimplemented!()
}

#[test]
fn test_matches_without_wildcard() {
    assert!(prefix_matches("/v1/publishers", "/v1/publishers"));
    assert!(prefix_matches("/v1/publishers", "/v1/publishers/abc-123"));
    assert!(prefix_matches("/v1/publishers", "/v1/publishers/abc/books"));

    assert!(!prefix_matches("/v1/publishers", "/v1"));
    assert!(!prefix_matches("/v1/publishers", "/v1/publishersBooks"));
    assert!(!prefix_matches("/v1/publishers", "/v1/parent/publishers"));
}

#[test]
fn test_matches_with_wildcard() {
    assert!(prefix_matches(
        "/v1/publishers/*/books",
        "/v1/publishers/foo/books"
    ));
    assert!(prefix_matches(
        "/v1/publishers/*/books",
        "/v1/publishers/bar/books"
    ));
    assert!(prefix_matches(
        "/v1/publishers/*/books",
        "/v1/publishers/foo/books/book1"
    ));

    assert!(!prefix_matches("/v1/publishers/*/books", "/v1/publishers"));
    assert!(!prefix_matches(
        "/v1/publishers/*/books",
        "/v1/publishers/foo/booksByAuthor"
    ));
}
```
