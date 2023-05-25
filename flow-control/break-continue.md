# break와 continue

* 루프를 일찍 나가려면 break를 사용합니다.&#x20;
* 다음 루프를 바로 시작하려면 continue를 사용합니다.&#x20;

continue과 break 모두 선택적으로 중첩된 루프에서 벗어나는 데 사용되는 레이블 인수를 받을 수 있습니다:

```rust
fn main() {
    let v = vec![10, 20, 30];
    let mut iter = v.into_iter();
    'outer: while let Some(x) = iter.next() {
        println!("x: {x}");
        let mut i = 0;
        while i < x {
            println!("x: {x}, i: {i}");
            i += 1;
            if i == 2 {
                break 'outer;
            }
        }
    }
}
```

위 예제는 내부의 `while` 루프를 2회 반복한 후 바깥 루프를 빠져나갑니다.
