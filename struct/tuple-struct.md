# 튜플 구조체

튜플을 값으로 하는 구조체는 필드 이름이 필요없는 경우 가볍게 사용할 때 유용합니다.&#x20;

```rust
struct Point(i32, i32);

fn main() {
    let p = Point(17, 23);
    println!("({}, {})", p.0, p.1);
}
```

튜플 구조체는 단일 필드의 래퍼 (wrapper)로 새로운 타잎(newtype)이라고 불리는 패턴을 위해 종종 사용합니다. 이는 어떤 타잎에 대한 트레이트를 구현하여 포함하면서 기능을 확장하기위한 방법이 됩니다.&#x20;

```rust
struct PoundsOfForce(f64);
struct Newtons(f64);

fn compute_thruster_force() -> PoundsOfForce {
    todo!("Ask a rocket scientist at NASA")
}

fn set_thruster_force(force: Newtons) {
    // ...
}

fn main() {
    let force = compute_thruster_force();
    set_thruster_force(force);
}
```

위는 `f64`에 대해 서로 다른 의미를 부여하기위해 `struct`로 감싼 구조라고 할 수 있습니다.&#x20;

발표자 노트의 설명입니다.&#x20;

* 뉴타입은 다음과 같은 원시타입 값에 특별한 의미를 부여하는 데 유용합니다.
  * 단위 표시를 위한 숫자: 위 예제에서는 뉴턴 단위 표기를 위해 사용합니다.
  * 값이 생성될 때 이미 유효성 검사를 통과 했으므로 추가적인 검사가 필요없는 경우: `PhoneNumber(String)`또는 `OddNumber(u32)`
* `Newtons` 타입의 값에 `f64` 값을 더하는 방법을 보여주세요.
  * 러스트는 대체로 분명하지 않은 것을 싫어합니다. 예를 들면 자동으로 unwrap하거나 불리언 값을 정수 값으로 사용하는 것들이 그렇습니다.
  * 연산자 재정의는 3일차 제네릭 부분에서 다룹니다.

<details>

<summary> 놀미 노트</summary>

튜플 구조체는 많이 사용하는 편은 아닌 듯 합니다. 새로운 타잎(newtype)도 보통은 다른 구조체를 포함한 구조체로 제공할 수 있기 때문입니다.

</details>
