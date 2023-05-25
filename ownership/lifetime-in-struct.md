# 구조체에서의 수명

어떤 타입이 빌려온 데이터를 저장하고 있다면, 반드시 수명을 표시해야 합니다:

```rust
#[derive(Debug)]
struct Highlight<'doc>(&'doc str);

fn erase(text: String) {
    println!("Bye {text}!");
}

fn main() {
    let text = String::from("The quick brown fox jumps over the lazy dog.");
    let fox = Highlight(&text[4..19]);
    let dog = Highlight(&text[35..43]);
    // erase(text);
    println!("{fox:?}");
    println!("{dog:?}");
}
```

<details>

<summary>발표자 노트</summary>

* 위의 예제에서 `Highlight`의 표식(`<'doc>`)은 적어도 `Highlight` 인스턴스가 살아있는 동안에는 그 내부의 `&str`가 가리키는 데이터 역시 살아있어야 한다는 것을 의미합니다.
* 만약 `text`가 `fox` (혹은 `dog`)의 수명이 다하기 전에 `erase`함수 호출 등으로 사라지게 된다면 빌림 검사기가 에러를 발생합니다.
* 빌린 데이터를 가지고 있는 타입은 사용자로 하여금 원본 데이터를 유지하도록 강제합니다. 이런 타입은 경량 뷰(lightweight view)를 만드는데 유용하지만, 이 제약 조건 때문에 이런 타입을 사용하는 것이 쉽지만은 않습니다.
* 따라서, 가능하다면, 구조체가 자신의 데이터를 직접 소유하도록 하는 것이 좋습니다.
* 한 구조체 안에 여러 참조가 있으면서, 이 참조들의 수명이 서로 다르게 지정되는 경우도 있습니다. 이는 참조와 그 구조체 간의 관계 뿐만이 아니라, 그 참조들 사이의 수명 관계를 설명해야 할 경우에 필요합니다. 매우 고급 기술입니다.

</details>
