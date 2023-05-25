# 트레이트 객체 (Trait Object)

트레이트 객체는 예를 들어 컬렉션에서 다양한 유형의 값을 허용합니다:

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

fn main() {
    let pets: Vec<Box<dyn Pet>> = vec![
        Box::new(Cat),
        Box::new(Dog { name: String::from("Fido") }),
    ];
    for pet in pets {
        println!("Hello {}!", pet.name());
    }
}
```
{% endcode %}

pets를 할당한 후의 메모리 배치는 다음과 같습니다.&#x20;

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

값이 어떤 구체적인 유형인지 불투명하기 때문에 트레이트 객체는 동적인 크기를 갖는    타잎입니다. 모든 동적인 크기를 갖는 타잎처럼 포인터를 통해서 사용해야 하고, 대표적인 예가 `&dyn SomeTrait`, `Box<dyn SomeTrait>`입니다.

<details>

<summary>발표자 노트</summary>

* 특정 트레이트를 구현하는 유형은 크기가 다를 수 있습니다. 따라서 위의 예제에서 `Vec<Pet>`과 같은 것을 가질 수 없습니다.
* **\[1]** `dyn Pet`은 `Pet`을 구현하는 동적 크기의 타입임을 컴파일러에 알려주는 방법입니다
* **\[2]** 이 예제에서 펫은 펫을 구현하는 객체에 대한 팻 포인터를 보유합니다. 팻 포인터는 실제 객체에 대한 포인터와 해당 특정 객체의 펫 구현에 대한 가상 메서드 테이블에 대한 포인터의 두 가지 구성 요소로 구성됩니다.
* 위의 예에서 다음 출력을 비교하세요.

```rust
    println!("{} {}", std::mem::size_of::<Dog>(), std::mem::size_of::<Cat>());
    println!("{} {}", std::mem::size_of::<&Dog>(), std::mem::size_of::<&Cat>());
    println!("{}", std::mem::size_of::<&dyn Pet>());
    println!("{}", std::mem::size_of::<Box<dyn Pet>>());
```

**\[1]** `dyn Pet`은 트레이트를 구현한 오브젝트에 대한 포인터와 같은 사용(이것이 트레이트 오브젝트)을 필요로 한다고 알려줍니다.

**\[2]** 팻 포인터는 길이나 가상 함수 테이블과 같은 추가 정보를 가진 포인터를 말합니다.

</details>

러스트 레퍼런스는 읽기 부담스러운 경우가 종종 있지만 확실한 답을 알고자 할 때는 가장 좋은 문서입니다. [트레이트 오브젝트](https://doc.rust-lang.org/reference/types/trait-object.html)에 대한 러스트 레퍼런스 내용을 한번 살펴보세요.
