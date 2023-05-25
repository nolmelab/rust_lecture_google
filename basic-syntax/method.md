# 메서드

메서드는 타입과 연관된 함수입니다. 메서드의 `self` 인자는 메서드가  구현하는 타잎의 인스턴스입니다:

```rust
struct Rectangle {
    width: u32,
    height: u32,
}

impl Rectangle {
    fn area(&self) -> u32 {
        self.width * self.height
    }

    fn inc_width(&mut self, delta: u32) {
        self.width += delta;
    }
}

fn main() {
    let mut rect = Rectangle { width: 10, height: 5 };
    println!("old area: {}", rect.area());
    rect.inc_width(5);
    println!("new area: {}", rect.area());
}
```

* 오늘과 내일 강의에서 더 많은 메서드 사용법을 다룰 것입니다.

<details>

<summary>발표자 노트</summary>

*   아래 `Rectangle::new` 생성자를 추가하고 `main`에서 호출하세요.

    ```rust
    fn new(width: u32, height: u32) -> Rectangle {
        Rectangle { width, height }
    }
    ```
* `Rectangle::new_square(width: u32)` 생성자를 추가하여 생성자가 임의의 파라미터를 받을 수 있다는 걸 보여주세요

</details>



