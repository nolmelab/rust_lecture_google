# 안전하지 않은 함수 작성하기 (writing unsafe function)

여러분이 작성한 함수를 사용할 때 어떤 특별한 조건(메모리  관련)을 만족해야 한다면, `unsafe`로 마킹할 수 있습니다.

```rust
/// Swaps the values pointed to by the given pointers.
///
/// # Safety
///
/// The pointers must be valid and properly aligned.
unsafe fn swap(a: *mut u8, b: *mut u8) {
    let temp = *a;
    *a = *b;
    *b = temp;
}

fn main() {
    let mut a = 42;
    let mut b = 66;

    // Safe because ...
    unsafe {
        swap(&mut a, &mut b);
    }

    println!("a = {}, b = {}", a, b);
}
```

<details>

<summary>발표자 노트</summary>

참조를 사용하면 안전하게 구현할 수 있기 때문에, 실제로 포인터를 사용할 필요는 없습니다.

unsafe 코드가 unsafe 함수의 내부에서 호출될 경우에는 `unsafe`블록을 지정하지 않아도 됩니다. `unsafe`블록을 항상 지정하도록 하고 싶다면 `#[deny(unsafe_op_in_unsafe_fn)]`를 이용하세요. 이 어트리뷰트를 추가해 보고 어떤 일이 일어나는지 확인해 보세요.

</details>
