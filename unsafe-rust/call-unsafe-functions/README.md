# 안전하지 않은 함수 호출 (call unsafe functions)

함수나 메서드가 정의되지 않은 동작(undefined behavior)으로 빠지지 않게 하기 위해서 만족해야 하는 전제 조건이 있는 경우, 그 함수나 메서드를 `unsafe`로 표시할 수 있습니다:

```rust
fn main() {
    let emojis = "🗻∈🌏";

    // Safe because the indices are in the correct order, within the bounds of
    // the string slice, and lie on UTF-8 sequence boundaries.
    unsafe {
        println!("emoji: {}", emojis.get_unchecked(0..4));
        println!("emoji: {}", emojis.get_unchecked(4..7));
        println!("emoji: {}", emojis.get_unchecked(7..11));
    }

    println!("char count: {}", count_chars(unsafe { emojis.get_unchecked(0..7) }));

    // Not upholding the UTF-8 encoding requirement breaks memory safety!
    // println!("emoji: {}", unsafe { emojis.get_unchecked(0..3) });
    // println!("char count: {}", count_chars(unsafe { emojis.get_unchecked(0..3) }));
}

fn count_chars(s: &str) -> usize {
    s.chars().map(|_| 1).sum()
}
```

`get_unchecked()` 함수가 unsafe 함수이고 호출하려면 unsafe 블록에 있어야 합니다.

