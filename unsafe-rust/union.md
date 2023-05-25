# Union

유니온 타입은 열거형(enum)과 비슷하지만, 어떤 필드에 해당하는 값을 가지고 있는지 여부를 프로그래머가 수동으로 추적해야 합니다:

```rust
#[repr(C)]
union MyUnion {
    i: u8,
    b: bool,
}

fn main() {
    let u = MyUnion { i: 42 };
    println!("int: {}", unsafe { u.i });
    println!("bool: {}", unsafe { u.b });  // Undefined behavior!
}
```

<details>

<summary>발표자 노트</summary>

러스트에는 열거형이 있기 때문에 유니온이 필요한 경우는 극히 드뭅니다. 유니온은 C 라이브러리 API를 사용할 때 가끔 필요합니다.

바이트들을 특정 타입으로 재해석 하고 싶다면 [`std::mem::transmute`](https://doc.rust-lang.org/stable/std/mem/fn.transmute.html)나 좀 더 안전한 [`zerocopy`](https://crates.io/crates/zerocopy) 크레이트를 사용하세요.

</details>
