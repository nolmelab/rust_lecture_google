# 데이터를 포함하는 열거형 (Variant Payloads)

Payload는 적재된 화물을 뜻합니다. 여러 분류에 대해  어떤 다른 타잎의 값을 가질 수 있도록 했습니다. 이는 열거형은 여러 상자로 나눠서 구분할 수 있도록 하고, 각 상자에 다른 타잎의 값들을 담을 수 있도록 했다고 생각하면 됩니다.&#x20;

{% code lineNumbers="true" %}
```rust
enum WebEvent {
    PageLoad,                 // Variant without payload
    KeyPress(char),           // Tuple struct variant
    Click { x: i64, y: i64 }, // Full struct variant
}

#[rustfmt::skip]
fn inspect(event: WebEvent) {
    match event {
        WebEvent::PageLoad       => println!("page loaded"),
        WebEvent::KeyPress(c)    => println!("pressed '{c}'"),
        WebEvent::Click { x, y } => println!("clicked at x={x}, y={y}"),
    }
}

fn main() {
    let load = WebEvent::PageLoad;
    let press = WebEvent::KeyPress('x');
    let click = WebEvent::Click { x: 20, y: 80 };

    inspect(load);
    inspect(press);
    inspect(click);
}
```
{% endcode %}

라인 17부터 19까지 열거형을 초기화 하는 방법과 라인 9의 패턴 일치문에서 상자들로부터 값을 얻는 방법을 잘 살펴보세요.&#x20;

이와 같이 분류된 여러 타잎의 값들을 갖는 구조는 매우 유용하고 실제로 많이 사용하고 있습니다. 러스트의 현대적 언어 기능의 핵심 중 하나입니다.&#x20;

<details>

<summary>발표자 노트</summary>

* 열거형 안의 값은 패턴 매칭이 되고 난 이후에만 접근 가능합니다. 그 값에 대한 레퍼런스는 `=>` 이후에 사용가능합니다.
  * 매치 패턴들은 위에서 아래로 순서에 따라 검사합니다. C나 C++에서와 같은 fall-through는 없습니다.
  * \[1] 매치 표현식 자체는 값을 가집니다. 그 값은 매칭이 된 패턴에서 가장 마지막에 수행된 표현식이 됩니다.
  * 가장 위에서 부터 어떤 패턴이 주어진 값과 매칭하는지 검사한 다음, 매칭된 것이 발견되면 화살표를 따라 코드를 수행합니다. 한 번 매칭이 되고 코드가 수행이 되면, 더이상의 매칭은 없습니다.
* 매칭 패턴들이 불충분 하다면 어떤 일이 일어나는지 설명하세요. 러스트 컴파일러는 모든 가능한 케이스들이 핸들링 되는지 체크한다는 점을 상기시키세요.
* `[2] match`는 주어진 열거형 값이 실제로 어떤 variant인지 판단하기 위해, 그 variant의 종류가 기록된, 숨겨진 필드(식별자)의 값을 검사합니다.
* `[3] std::mem::discriminant()`를 이용하여 식별자를 얻을 수도 있습니다.
  * 이는 각 필드 값을 굳이 비교할 필요 없는 구조체에 대해 `PartialEq` 트레잇을 구현할 때 유용합니다.
* `[4] WebEvent::Click { ... }`은 최상위 레벨 구조체 `struct Click {...}`를 따로 정의하고 `WebEvent::Click(Click)`처럼 튜플 형태로 정의한 것과 정확히 같진 않습니다. 예를 들어 `WebEvent::Click { ... }` 로 정의한 경우, 구조체 형태와 유사하지만 트레이트를 구현 할 수 없습니다.

</details>

<details>

<summary>놀미 노트</summary>

\[1] 러스트는 다른  언어의 문장(statement)들이 표현식(expression)입니다. 표현식은 값으로 계산되는 문법 단위입니다. match의 => 문장도 표현식에 해당하므로 값을 얻을 수 있습니다. 이는 match 결과를 변수에 할당하거나 리턴할 수 있게 하여 코딩을 편하게 합니다.&#x20;

\[2] / \[3] 열거형 내부적으로 관리하는 식별자 변수가 있다는 뜻으로 이해됩니다. `enum`의 메모리 크기를 잘 살펴보면 찾을 수 있을 듯 합니다. `std::mem::size_of<WebEvent>()`로 크기를 얻을 수 있습니다. 더 자세한 내용은 [러스트 열거형 매치 코드 생성](https://www.eventhelix.com/rust/rust-to-assembly-enum-match/)에서 살펴볼 수 있습니다.&#x20;

\[4] 구조체를 열거형에 직접 포함할 경우 `impl`을 할 수 없습니다. 이는 자명한데 구현이 필요할 경우 분리하면 된다고 알려주려는 의도인 듯 합니다.&#x20;

</details>
