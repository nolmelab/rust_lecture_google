# 정적 가변(mutable) 변수

불변 정적변수를 읽는 것은 안전합니다:

```rust
static HELLO_WORLD: &str = "Hello, world!";

fn main() {
    println!("HELLO_WORLD: {HELLO_WORLD}");
}
```

하지만, 데이터 레이스가 발생할 수 있으므로 정적 가변변수를 읽고 쓰는 것은 안전하지 않습니다:

```rust
static mut COUNTER: u32 = 0;

fn add_to_counter(inc: u32) {
    unsafe { COUNTER += inc; }  // Potential data race!
}

fn main() {
    add_to_counter(42);

    unsafe { println!("COUNTER: {COUNTER}"); }  // Potential data race!
}
```

<details>

<summary>발표자 노트</summary>

일반적으로 이야기 해서, 정적 가변 변수를 쓰는 것은 좋은 아이디어가 아닙니다. 그러나 `no_std`와 같은 저수준 코딩을 할 경우에는 필요하기도 합니다. 예를 들어 힙 할당기를 구현하거나, C API를 사용하는 게 그런 경우입니다.

</details>
