# 복사(Copy)와 복제(Clone)

이동이 기본 설정이지만, 특정 타입은 복사됩니다:

```rust
fn main() {
    let x = 42;
    let y = x;
    println!("x: {x}");
    println!("y: {y}");
}
```

이러한 타입들은 Copy 트레잇을 구현합니다.

직접 만든 타입들도 Copy트레잇을 구현하여 복사를 할 수 있습니다:

```rust
#[derive(Copy, Clone, Debug)]
struct Point(i32, i32);

fn main() {
    let p1 = Point(3, 4);
    let p2 = p1;
    println!("p1: {p1:?}");
    println!("p2: {p2:?}");
}
```

* 할당 후, p1와 p2는 자신의 데이터를 소유합니다.
* 명시적으로 p1.clone()를 사용하여 데이터를 복사할 수 있습니다.

<details>

<summary>발표자 노트</summary>

복사(copy)와 복제(clone)는 같지 않습니다:

* 복사는 메모리의 내용을 그대로 한 벌 더 만드는 것을 의미하며, 아무 객체에서나 다 지원하지는 않습니다.
* 복사는 커스터마이즈 할 수 없습니다. (C++에서 복사 생성자를 통해 복사 동작을 임의로 구현할 수 있는 것과 비교가 됩니다.)
* 복제는 보다 일반적인 작업이며, Clone트레잇을 구현하여 복제시 동작을 커스터마이즈 할 수 있습니다.
* Drop 트레이트를 구현한 타입은 복사되지 않습니다.

위의 예시에서 다음을 시도해 보시기 바랍니다:

* Point구조체에 String필드를 추가하세요. 컴파일 되지 않을 것입니다. 왜냐하면 String은 Copy트레잇을 구현하고 있지 않기 때문입니다.
* derive 속성에서 Copy를 제거해 보세요. p1을 println! 할 때 컴파일 에러가 발생할 것입니다.
* p1을 복제하면 잘 동작함을 확인해 보세요.

만약 학생들이 derive에 대해 묻는다면, 컴파일 시 러스트에서 코드를 생성하는 방법이라고 말하는 것으로 충분합니다. 위 경우 Copy와 Clone 트레잇에 대한 기본 구현이 생성됩니다.

</details>

<details>

<summary>언습</summary>

* Drop이 가능하면 왜 복사가 안 될까요?

</details>
