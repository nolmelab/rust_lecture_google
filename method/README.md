# 메서드 (Method)

메서드는 클래스가 있는 언어의 멤버 함수에 해당합니다. 러스트에서는 impl 타잎 블록에 함수들을 작성하고 이들을 메서드라고 부릅니다.&#x20;

{% code lineNumbers="true" %}
```rust
#[derive(Debug)]
struct Person {
    name: String,
    age: u8,
}

impl Person {
    fn say_hello(&self) {
        println!("Hello, my name is {}", self.name);
    }
}

fn main() {
    let peter = Person {
        name: String::from("Peter"),
        age: 27,
    };
    peter.say_hello();
}
```
{% endcode %}

<details>

<summary>발표자 노트</summary>

* 메서드를 함수와 비교하여 소개하는 것도 도움이 될 수 있습니다.
  * 메서드는 구조체나 열거형과 같은 타입의 인스턴스에서 호출 되며, 첫번째 매개변수(파라메터)는 인스턴스를 `self`로 표기합니다.
  * **\[1]** 메서드를 이용하면 receiver 문법을 사용할 수 있고 코드를 좀더 체계적으로 정리할 수 있습니다. 메서드들이 예측 가능한 위치에 모여 있으니 찾기 쉽습니다.

<!---->

* 메서드 수신자(receiver)인 `self` 키워드 사용을 언급해 주시기 바랍니다.
  * 예제의 경우 `self: &Self`의 줄인 버전임을 알려주고, 구조체의 이름을 직접 사용하면 어떻게 되는지 보여주는 것도 좋습니다.
  * `impl` 블록 내부에서는 `Self`가 해당 타입의 이름 대용으로 사용될 수 있음을 알려주세요.
  * 구조체의 필드를 접근할 때 점 표기를 사용하듯이 `self`에 점 표기를 사용하여 개별 필드들을 접근할 수 있습니다.
  * `say_hello` 함수가 두 번 호출되도록 코드를 수정하여 `&self`와 `self`가 어떻게 다른지 보여주는 것도 좋습니다.

<!---->

* 다음 슬라이드에서 수신자(receiver)의 구분을 설명합니다.

</details>

<details>

<summary>놀미 노트</summary>

**\[1]** 수신자(receiver)라고 부르는 점이 특이합니다. `self, mut self, &self, &mut self`가 수신자가 될 수 있고 `Self` 타잎이며 `Self`는 `impl 타잎`의 타잎과 같습니다. 예제 코드에서는 `Person`이 `Self`입니다.&#x20;

</details>
