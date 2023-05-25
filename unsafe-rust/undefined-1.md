# 안전하지 않은 트레이트 구현

함수에서와 마찬가지로 트레이트도 `unsafe`로 마킹 가능합니다. 만약 그 트레이트를 구현할 때 정의되지 않은 동작을 피하기 위해 특별한 조건이 필요하다면 말이지요.

예를 들어 `zerocopy` 크레이트에는 [안전하지 않은 트레잇](https://docs.rs/zerocopy/latest/zerocopy/trait.AsBytes.html)이 있습니다:

```rust
use std::mem::size_of_val;
use std::slice;

/// ...
/// # Safety
/// The type must have a defined representation and no padding.
pub unsafe trait AsBytes {
    fn as_bytes(&self) -> &[u8] {
        unsafe {
            slice::from_raw_parts(self as *const Self as *const u8, size_of_val(self))
        }
    }
}

// Safe because u32 has a defined representation and no padding.
unsafe impl AsBytes for u32 {}
```

<details>

<summary>발표자 노트</summary>

안전하지 않은 트레잇을 만들 때에는 주석에 `# Safety` 항목이 있어서 이 트레잇을 안전하게 구현하려면 어떤 요구사항들을 만족해야 하는지를 설명해야 합니다.

`AsBytes`에서 지켜야 할 안전성에 대한 실제 설명은 좀 더 길고 복잡합니다.

빌트인 트레잇인 `Send`와 `Sync`는 안전하지 않은 트레잇 입니다.

</details>
