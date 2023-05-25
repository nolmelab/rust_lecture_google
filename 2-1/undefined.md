# 건강상태 모니터링 시스템

당신은 건강 상태를 모니터링하는 시스템을 구현하는 일을 하고 있습니다. 그 일환으로 당신은 사용자의 건강 상태 통계를 추적해야합니다.

당신의 목표는 `User` 구조체의 `impl` 블록의 빈 함수를 구현하는 것입니다.

아래 코드를 [https://play.rust-lang.org/](https://play.rust-lang.org/)에 복사해서 빠진 메서드를 구현하면 됩니다:

```rust
// TODO: remove this when you're done with your implementation.
#![allow(unused_variables, dead_code)]

struct User {
    name: String,
    age: u32,
    weight: f32,
}

impl User {
    pub fn new(name: String, age: u32, weight: f32) -> Self {
        unimplemented!()
    }

    pub fn name(&self) -> &str {
        unimplemented!()
    }

    pub fn age(&self) -> u32 {
        unimplemented!()
    }

    pub fn weight(&self) -> f32 {
        unimplemented!()
    }

    pub fn set_age(&mut self, new_age: u32) {
        unimplemented!()
    }

    pub fn set_weight(&mut self, new_weight: f32) {
        unimplemented!()
    }
}

fn main() {
    let bob = User::new(String::from("Bob"), 32, 155.2);
    println!("I'm {} and my age is {}", bob.name(), bob.age());
}

#[test]
fn test_weight() {
    let bob = User::new(String::from("Bob"), 32, 155.2);
    assert_eq!(bob.weight(), 155.2);
}

#[test]
fn test_set_age() {
    let mut bob = User::new(String::from("Bob"), 32, 155.2);
    assert_eq!(bob.age(), 32);
    bob.set_age(33);
    assert_eq!(bob.age(), 33);
}
```

플레이 그라운드 보다는 vscode나 사용할 에디터/IDE에서 작성하길 권고 드립니다.&#x20;

