# 통합 테스트 (integration test)

라이브러리를 사용자 입장에서 테스트 하려면, 통합 테스트를 해야 합니다.

`test/`디렉터리 아래에 `.rs`파일을 하나 만드세요:

```rust
use my_library::init;

#[test]
fn test_init() {
    assert!(init().is_ok());
}
```

이 테스트는 크레이트의 공개 API에만 접근할 수 있습니다.
