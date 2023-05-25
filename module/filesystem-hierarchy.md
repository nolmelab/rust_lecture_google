# 파일 시스템 계층 (Filesystem Hierarchy)

모듈 내용을 생략하고 파일에 정의하는 것이 가능합니다.&#x20;

```rust
mod garden;
```

`garden` 모듈 콘텐츠는 다음에서 찾을 수 있습니다:

* `src/garden.rs` (최신 Rust 2018 스타일)&#x20;
* `src/garden/mod.rs`(구형 Rust 2015 스타일)&#x20;

마찬가지로 `garden::vegetables` 모듈은 다음 위치에서 찾을 수 있습니다:

* `src/garden/vegetables.rs` (최신 Rust 2018 스타일)&#x20;
* `src/garden/vegetables/mod.rs` (구형 Rust 2015 스타일)

crate 루트는 다음에 있습니다:

* `src/lib.rs`(라이브러리 크레이트의 경우)&#x20;
* `src/main.rs`(바이너리 크레이트의 경우)

파일에 정의된 모듈도 "내부 문서 주석"을 사용하여 문서화할 수 있습니다. 이 주석은 해당 주석이 포함된 항목(이 경우 모듈)을 문서화합니다.

```rust
//! This module implements the garden, including a highly performant germination
//! implementation.

// Re-export types from this module.
pub use seeds::SeedPacket;
pub use garden::Garden;

/// Sow the given seed packets.
pub fn sow(seeds: Vec<SeedPacket>) { todo!() }

/// Harvest the produce in the garden that is ready.
pub fn harvest(garden: &mut Garden) { todo!() }
```

모듈 이름의 폴더에  mod.rs 파일을 두는 2015 이전 스타일에서 2018 스타일로 변경한 이유는 너무 많은 파일이 mod.rs가 되어 IDE에서 보기 어렵게 만드는 걸 피하기 위해서 입니다. 여전히 모듈 이름의 폴더에 여러 하위 모듈을 둘 수 있습니다.&#x20;

