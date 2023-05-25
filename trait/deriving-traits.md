# 트레이트 상속하기 (Deriving Traits)

컴파일러가 여러가지 트레잇을 상속(derive)하도록 할 수 있습니다. 이 경우 컴파일러가 트레잇을 자동으로 구현합니다:

```rust
#[derive(Debug, Clone, PartialEq, Eq, Default)]
struct Player {
    name: String,
    strength: u8,
    hit_points: u8,
}

fn main() {
    let p1 = Player::default();
    let p2 = p1.clone();
    println!("Is {:?}\nequal to {:?}?\nThe answer is {}!", &p1, &p2,
             if p1 == p2 { "yes" } else { "no" });
}
```

트레이트를 상속한다는 뜻은 트레이트를 impl 한다는 뜻입니다. derive 속성은 매크로 기능을 통해 이들 impl을 주어진 트레이트에 대해 생성해줍니다.&#x20;
