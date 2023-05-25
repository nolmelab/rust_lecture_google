# 원시 포인터 역참조 (따라가기)

포인터를 만드는 것은 안전합니다. 하지만 역참조(따라가기)할 경우 `unsafe`가 필요합니다:

```rust
fn main() {
    let mut num = 5;

    let r1 = &mut num as *mut i32;
    let r2 = r1 as *const i32;

    // Safe because r1 and r2 were obtained from references and so are
    // guaranteed to be non-null and properly aligned, the objects underlying
    // the references from which they were obtained are live throughout the
    // whole unsafe block, and they are not accessed either through the
    // references or concurrently through any other pointers.
    unsafe {
        println!("r1 is: {}", *r1);
        *r1 = 10;
        println!("r2 is: {}", *r2);
    }
}
```

<details>

<summary>발표자 노트</summary>

모든 `unsafe` 블록에 대해 왜 그 코드가 안전한지에 대한 설명을 주석으로 다는 것은 좋은 습관입니다(사실 안드로이드의 러스트 스타일 가이드에서는 이게 필수입니다).

포인터 역참조를 할 경우, 포인터가 [_유효_](https://doc.rust-lang.org/std/ptr/index.html#safety)해야 합니다. 예를 들어:

* 포인터는 null이면 안됩니다.
* 포인터는 역참조가 가능해야 합니다 (객체의 어느 한 부분을 가리키고 있어야 합니다).
* 이미 반환된 객체를 가리키면 안됩니다.
* 같은 위치에 대해 동시적인 접근이 있으면 안됩니다.
* 참조를 캐스팅 해서 포인터를 만들었다면, 그 참조가 가리키는 객체는 살아 있어야 하며, 그 객체의 메모리를 접근하는 참조가 하나도 없어야 합니다.

대부분의 경우 포인터는 align되어 있어야 합니다.

</details>
