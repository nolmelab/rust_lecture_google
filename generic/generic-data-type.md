# 제네릭 데이터 타잎 (Generic Data Type)

제네릭을 사용하여 필드의 타잎을 추상화 할 수 있습니다.&#x20;

```rust
#[derive(Debug)]
struct Point<T> {
    x: T,
    y: T,
}

fn main() {
    let integer = Point { x: 5, y: 10 };
    let float = Point { x: 1.0, y: 4.0 };
    println!("{integer:?} and {float:?}");
}
```

<details>

<summary>발표자 노트</summary>

* `let p = Point { x : 5, y : 10.0 }` 새로운 변수 선언을 시도해보세요
* 다양한 유형의 요소를 가진 `Point`를 허용하도록 코드를 수정합니다.

</details>
