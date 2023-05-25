# 트레이트 (Trait)

트레잇은 타입을 추상화 하는데 사용됩니다. 인터페이스와 매우비슷합니다:

{% code lineNumbers="true" %}
```rust
trait Pet {
    fn name(&self) -> String;
}

struct Dog {
    name: String,
}

struct Cat;

impl Pet for Dog {
    fn name(&self) -> String {
        self.name.clone()
    }
}

impl Pet for Cat {
    fn name(&self) -> String {
        String::from("The cat") // No name, cats won't respond to it anyway.
    }
}

fn greet<P: Pet>(pet: &P) {
    println!("Who's a cutie? {} is!", pet.name());
}

fn main() {
    let fido = Dog { name: "Fido".into() };
    greet(&fido);

    let captain_floof = Cat;
    greet(&captain_floof);
}
```
{% endcode %}

라인 11과 17에 트레이트를 구현하는 방법이 있습니다. `impl ... for`는 어떤 대상에 어떤 특성을 부여하도록 구현한다는 뜻으로 상속보다 더 명확해 보입니다.&#x20;

라인 23에 트레이트로 제약된 제네릭 함수를 구현한 예시가 있습니다. 라인 29와 32에서 사용합니다.&#x20;

