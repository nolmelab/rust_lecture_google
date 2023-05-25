# 매치 가드

패턴 뒤에 가드(guard, 조건식)를 덧붙일 수 있습니다. 가드는 패턴이 매치되면 추가로 따져보는 불리언 표현식입니다:

{% code lineNumbers="true" %}
```rust
#[rustfmt::skip]
fn main() {
    let pair = (2, -2);
    println!("Tell me about {pair:?}");
    match pair {
        (x, y) if x == y     => println!("These are twins"),
        (x, y) if x + y == 0 => println!("Antimatter, kaboom!"),
        (x, _) if x % 2 == 1 => println!("The first one is odd"),
        _                    => println!("No correlation..."),
    }
}
```
{% endcode %}

매치 가드의 `if` 문은 매칭의 가지를 구성합니다. 라인 6과 라인 7은 `(x, y)`는 동일하지만 `if` 문이 달라 서로 다른 패턴과 일치됩니다.

<details>

<summary>발표자 노트</summary>

* 매치 가드는 별도의 문법 요소로서 패턴 자체만으로 표현하기 어려운 복잡한 경우를 간결하게 표현하고자 할 때 유용합니다.
* 매치의 각 팔(혹은 가지) 안에 따로 `if`를 사용한 것과 다릅니다. 매치 가지의 `=>` 뒤에 사용된 `if` 표현식은 해당 가지가 선택된 다음에 실행됩니다. 따라서 여기서 `if` 조건이 실패하더라도 원래 `match`의 다른 가지는 고려되지 않습니다.
* 패턴에 정의된 변수를 가드의 표현식에서 사용할 수 있습니다.
* **\[1]** 가드에 정의된 조건은 `|` 를 포함하는 패턴의 모든 표현식에 적용됩니다.

**\[1]** 실제 사용할 때 깜빡하기 쉬운 조건으로 보입니다.

</details>
