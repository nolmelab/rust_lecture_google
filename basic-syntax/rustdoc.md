# rustdoc

러스트는 ///로 문서화를 합니다.

```rust
/// Determine whether the first argument is divisible by the second argument.
///
/// If the second argument is zero, the result is false.
fn is_divisible_by(lhs: u32, rhs: u32) -> bool {
    if rhs == 0 {
        return false;  // Corner case, early return
    }
    lhs % rhs == 0     // The last expression in a block is the return value
}
```

콘텐츠는 마크다운으로 처리됩니다. 게시된 모든 Rust 라이브러리 크레이트는 rustdoc 도구를 사용하여 docs.rs에 자동으로 문서화됩니다. 이 패턴을 사용하여 API의 모든 공개 항목을 문서화합니다.&#x20;

<details>

<summary>발표자 노트</summary>

* 학생들에게 rand 크레이트에서 생성한 docs.rs/rand를 보여주세요.
* 이 과정에서는 공간을 절약하기 위해 슬라이드에 rustdoc을 포함하지 않았지만 실제 코드는 반드시 포함해야 합니다.

</details>

<details>

<summary>놀미 노트</summary>

* &#x20;//!는 주석이 있는 곳의 상위 단위에 대한 문서화입니다. 예를 들어, 모듈 안에 있으면 모듈에 대한 문서화입니다.

</details>
