# 필드 할당 단축문법 (Field Shorthand Syntax)

구조체의 필드와 동일한 이름의 변수가 있다면 "짧은 문법"으로 구조체를 생성할 수 있습니다.&#x20;

```rust
#[derive(Debug)]
struct Person {
    name: String,
    age: u8,
}

impl Person {
    fn new(name: String, age: u8) -> Person {
        Person { name, age }
    }
}

fn main() {
    let peter = Person::new(String::from("Peter"), 27);
    println!("{peter:?}");
}
```

Person을 만드는 new() 함수는 러스트의 관용적인 생성자 함수입니다. 러스트에는 별도로 정해진 생성자 문법이 없습니다. 이와 같이 하는 것으로 충분하기 때문입니다.&#x20;

impl 블럭은 Self를 현재 대상 구조체나 enum의 타잎으로 제공합니다. 따라서 new() 함수를 다음과 같이 할 수 있습니다.&#x20;

```rust
impl Person {
    fn new(name: String, age: u8) -> Self {
        Self { name, age }
    }
}
```

기본 값을 제공하는 default() 함수가 있는 트레이트가 Default입니다. 이를 구현하면 기본 값을 사용할 수 있도록 할 수 있습니다.&#x20;

{% code lineNumbers="true" %}
```rust
#[derive(Debug)]
struct Person {
    name: String,
    age: u8,
}
impl Default for Person {
    fn default() -> Person {
        Person {
            name: "Bot".to_string(),
            age: 0,
        }
    }
}
fn create_default() {
    let tmp = Person {
        ..Default::default()
    };
    let tmp = Person {
        name: "Sam".to_string(),
        ..Default::default()
    };
}
```
{% endcode %}

라인 6부터 13까지 Default 트레이트를 Person에 대해 구현하는 코드입니다. 트레이트의 구현은 여기가 처음인 듯 합니다. 다른 언어의 인터페이스 구현과 거의 동일합니다.&#x20;

create\_default() 함수의 16, 20 라인에서 Default 트레이트를 사용합니다. 러스트가 Default::default를 Person에 대해 어떻게 추론할 수 있는지 한번 생각해 보세요.&#x20;

발표자 노트의 일부 내용입니다.&#x20;

* `peter`와 구조체 업데이트 문법을 사용하여 새로운 구조체 인스턴스를 만들어보세요. 이때, `peter`는 더이상 사용할 수 없게 됩니다.
* 구조체를 `Debug` 형태로 출력하려면 `{:#?}`를 사용하세요.

"구조체 업데이트 문법"은 어떤 것일까요? 여기서는 새로운 타잎 (newtype) 패턴을 적용하는 것으로 보입니다.&#x20;

`{:#?}`에서 `#?`는 예쁘게 출력하라는 플래그입니다. [`std::fmt::Debug`](https://doc.rust-lang.org/std/fmt/trait.Debug.html) 내용을 한번 읽어 보세요.

<details>

<summary>놀미 노트</summary>

자바스크립트와 같은 동적인 언어에서 주로 제공하는 기능으로 편리한 면이 있으나 자주 사용할 기능은 아닌 듯 합니다. 다른 코드를 읽을 때 알고 있어야 하는 정도로 생각하면 되겠습니다.

</details>

