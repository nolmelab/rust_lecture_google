# 제네릭 메서드 (Generic Method)

일반 메서드 또는 일반 함수라고 부르고 싶습니다.&#x20;

```rust
#[derive(Debug)]
struct Point<T>(T, T);

impl<T> Point<T> {
    fn x(&self) -> &T {
        &self.0  // + 10
    }

    // fn set_x(&mut self, x: T)
}

fn main() {
    let p = Point(5, 10);
    println!("p.x = {}", p.x());
}
```

<details>

<summary>발표자 노트</summary>

* _질문:_ `impl<T> Point<T> {}`에서 `T`가 왜 두 번 사용됩니까?
  * 제네릭 타입에 대한 제네릭 구현 이기 때문입니다. 이 두 제네릭은 서로 독립적입니다.
  * 이는 임의의 모든 `T`에 대해서 이 메소드들이 정의된다는 것을 의미합니다.
  * **`[1]`**` ``impl Point<u32> { .. }`와 같이 작성하는 것도 가능합니다.
    * `Point`는 여전히 제네릭이며 `Point<f64>`를 사용할 수도 있지만 이 블록의 메서드는 `Point<u32>`만 쓸 수 있습니다.

**\[1]** 템플릿 특수화라고 불리는 기능과 비슷하게 특정 타잎에 대한 코드를 별도로 정의할 수 있습니다. 러스트는 개념을 단순화하여 강력하게 만드는 방향을 기본 흐름으로 갖고 있습니다.

</details>
