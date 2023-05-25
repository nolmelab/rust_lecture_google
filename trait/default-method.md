# 기본 메서드 (Default Method)

트레이트의 디폴트 메서드에서 다른(구현되지 않은) 메소드를 이용할 수 있습니다:

```rust
trait Equals {
    fn equal(&self, other: &Self) -> bool;
    fn not_equal(&self, other: &Self) -> bool {
        !self.equal(other)
    }
}

#[derive(Debug)]
struct Centimeter(i16);

impl Equals for Centimeter {
    fn equal(&self, other: &Centimeter) -> bool {
        self.0 == other.0
    }
}

fn main() {
    let a = Centimeter(10);
    let b = Centimeter(20);
    println!("{a:?} equals {b:?}: {}", a.equal(&b));
    println!("{a:?} not_equals {b:?}: {}", a.not_equal(&b));
}
```

기본 메서드들은 별도의 `impl` 블록이 아닌 `trait` 블록 안에 정의합니다.

## 트레이트의 부모 트레이트

러스트는 상속을 갖고 있지 않습니다. 대신 부모 트레이트 (Supertrait)를 지정하여 여러 특성을 갖도록 할 수 있습니다.&#x20;

러스트 예제 책에 있는 [SuperTrait ](https://doc.rust-lang.org/rust-by-example/trait/supertraits.html)문서입니다.&#x20;

{% code lineNumbers="true" %}
```rust
trait Person {
    fn name(&self) -> String;
}

// Person is a supertrait of Student.
// Implementing Student requires you to also impl Person.
trait Student: Person {
    fn university(&self) -> String;
}

trait Programmer {
    fn fav_language(&self) -> String;
}

// CompSciStudent (computer science student) is a subtrait of both Programmer 
// and Student. Implementing CompSciStudent requires you to impl both supertraits.
trait CompSciStudent: Programmer + Student {
    fn git_username(&self) -> String;
}

fn comp_sci_student_greeting(student: &dyn CompSciStudent) -> String {
    format!(
        "My name is {} and I attend {}. My favorite language is {}. My Git username is {}",
        student.name(),
        student.university(),
        student.fav_language(),
        student.git_username()
    )
}

fn main() {}
```
{% endcode %}

위 코드를 찬찬히 살펴보면 트레이트를 확장해 나가는 방법을 알 수 있습니다. 라인 21에 `&dyn CompSciStudent`로 임의의 트레이트 오브젝트를 받아 동적인 디스패치를 통해 처리할 수 있다는 걸 알 수 있습니다.

<details>

<summary>발표자 노트</summary>

* 트레이트는 미리 구현된(기본) 메서드와 사용자가 직접 구현해야 하는 메서드를 지정할 수 있습니다. 기본 구현이 있는 메서드는 필수 메서드에 의존할 수 있습니다.
* 메서드 not\_equal을 새 특성 NotEqual로 옮겨 보세요.
* NotEqual을 Equal의 슈퍼 트레이트로 만들어보세요.
*

</details>
