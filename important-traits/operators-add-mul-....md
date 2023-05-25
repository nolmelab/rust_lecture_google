# Operators : Add, Mul, ...

연산자는 `std::ops`에 있는 다양한 트레잇들을 통해 구현됩니다:

```rust
#[derive(Debug, Copy, Clone)]
struct Point { x: i32, y: i32 }

impl std::ops::Add for Point {
    type Output = Self;

    fn add(self, other: Self) -> Self {
        Self {x: self.x + other.x, y: self.y + other.y}
    }
}

fn main() {
    let p1 = Point { x: 10, y: 20 };
    let p2 = Point { x: 100, y: 200 };
    println!("{:?} + {:?} = {:?}", p1, p2, p1 + p2);
}
```

Add가 Rhs 타잎은 다르게 지정하여 구현할 수 있습니다. Point가 아닌 것들과 더할 수 있도록 구현할 수 있다는 뜻입니다.

```rust
pub trait Add<Rhs = Self> {
    /// The resulting type after applying the `+` operator.
    type Output;
    fn add(self, rhs: Rhs) -> Self::Output;
}
```

<details>

<summary>발표자 노트</summary>

* **\[1]** `&Point`가 `Add`를 구현하도록 할 수도 있습니다. 이게 어떤 경우에 유용할까요?
  * 답: `Add:add`는 `self`를 소모합니다. 만약 타입 `T`가 `Copy`트레잇을 구현하고 있지 않다면 `&T`에 대해서도 연산자 오버로딩을 고려해야 합니다. 이렇게 하면 호출부에서 불필요한 복사를 피할 수 있습니다.
* **\[2]** 왜 `Output`이 연관된 타입인가요? 타입 파라메터로 만들 수 있을까요?
  * 답: 타입 파라메터를 호출하는 쪽에서 결정합니다. 반면 연관된 타입(`Output`같은) 은 트레잇을 구현하는 쪽에서 제어 가능합니다.

**\[1]** self를 수신자 (Receiver)로 하기 때문에 이동하여 소멸됩니다. \&T에 대해 Add를 구현하려면 어떻게 하면 될까요?

**\[2]** 연관된 타잎(associated type)은 트레이트 내부에 정의한 타잎 이름으로 발표자 노트에 설명한 대로 외부에서 지정하지 않고 구현하는 쪽에서 지정하는 용도가 필요할 때 사용합니다.

</details>
