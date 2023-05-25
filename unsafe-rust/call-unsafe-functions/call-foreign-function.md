# 외부 코드 호출 (Call foreign function)

다른 언어의 함수는 러스트의 보증을 위반할 수 있습니다. 따라서 이를 호출하는 것은 안전하지 않습니다:

```rust
extern "C" {
    fn abs(input: i32) -> i32;
}

fn main() {
    unsafe {
        // Undefined behavior if abs misbehaves.
        println!("Absolute value of -3 according to C: {}", abs(-3));
    }
}
```

이게 문제가 되는 경우는 대부분 외부 함수가 러스트의 메모리 모델을 위반하고 있을 경우입니다. 그러나 어떤 C함수라도 어떤 임의의 상황에서는 정의되지 않은 동작을 할 수 있기 때문에, 엄밀히 말해서는 모든 외부 함수에 대해서 문제입니다.

위 예제 코드에서 `"C"`는 ABI를 의미합니다. [다른 ABI도 있습니다.](https://doc.rust-lang.org/reference/items/external-blocks.html)
