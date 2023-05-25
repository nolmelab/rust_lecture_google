# while 반복문

while 키워드는 다른 언어와 매우 유사하게 작동합니다:

```rust
fn main() {
    let mut x = 10;
    while x != 1 {
        x = if x % 2 == 0 {
            x / 2
        } else {
            3 * x + 1
        };
    }
    println!("Final x: {x}");
}
```

