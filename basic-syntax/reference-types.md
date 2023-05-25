# 참조 (Reference Types)

C++와 마찬가지로 러스트도 참조형을 갖습니다:

```rust
fn main() {
    let mut x: i32 = 10;
    let ref_x: &mut i32 = &mut x;
    *ref_x = 20;
    println!("x: {x}");
}
```

참고사항:

* `ref_x`에 값을 할당할 때, C/C++의 포인터와 유사하게 `*`를 이용해서 참조를 따라가야(역참조) 합니다.
* 러스트는 특정한 경우(메서드 호출)에 자동으로 역참조를 합니다.(`ref_x.count_one()`을 하면 `*ref_x`가 `count_one`의 인자로 전달됩니다.)
* `mut`로 선언된 참조는 그 변수가 살아있는 동안 다른 값을 가질 수 있습니다.
