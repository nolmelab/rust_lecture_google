# 구조체 (struct)

C/C++와 마찬가지로 러스트는 구조체를 지원합니다.&#x20;

{% code lineNumbers="true" %}
```rust
struct Person {
    name: String,
    age: u8,
}

fn main() {
    let mut peter = Person {
        name: String::from("Peter"),
        age: 27,
    };
    println!("{} is {} years old", peter.name, peter.age);
    
    peter.age = 28;
    println!("{} is {} years old", peter.name, peter.age);
    
    let jackie = Person {
        name: String::from("Jackie"),
        ..peter
    };
    println!("{} is {} years old", jackie.name, jackie.age);
}
```
{% endcode %}

러스트의 구조체는 C의 구조체와 구조는 비슷하고 역할은 C++의 클래스에 가깝습니다. 상속이 없다는 점은 클래스와 가장 큰 차이입니다.&#x20;

클래스의  멤버 함수에 해당하는 메서드는 impl 블럭에 따로 정의합니다. 이는 C 언어의 구조체와 구조체 연관 함수의 구조화에 더 개념적으로 가깝다고 볼 수 있습니다.&#x20;

라인 7처럼 필드의 값을 지정하여 구조체를 생성합니다. 라인 18의 ..peter는 peter에서 값을 가져와서 초기화합니다.&#x20;

러스트는 크기가 0인 구조체를 아래와 같이 만들 수 있습니다.&#x20;

```rust
struct Foo;
```

이는 러스트에서 프로그램 개념화/추상화/구조화의 핵심인 트레이트를 `Foo`에 대해 구현 가능하도록 합니다.&#x20;

