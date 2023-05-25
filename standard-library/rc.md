# Rc

[`Rc`](https://doc.rust-lang.org/std/rc/struct.Rc.html)는 참조 카운팅 공유 포인터입니다. 여러 위치에서 동일한 데이터를 참조해야 할 경우 사용합니다:

```rust
use std::rc::Rc;

fn main() {
    let mut a = Rc::new(10);
    let mut b = Rc::clone(&a);

    println!("a: {a}");
    println!("b: {b}");
}
```

* `Rc`내부의 데이터를 변경해야 하는 경우, 데이터를 [`Cell` 또는 `RefCell`](https://doc.rust-lang.org/std/cell/index.html)로 래핑해야합니다.
* 멀티스레드인 경우 [`Arc`](https://google.github.io/comprehensive-rust/ko/concurrency/shared\_state/arc.html)를 참조하시기 바랍니다.
* drop 가능한 순환 구조를 만들기 위해 공유 포인터를 [`Weak`](https://doc.rust-lang.org/std/rc/struct.Weak.html) 포인터로 **다운그레이드**할 수도 있습니다.

{% code lineNumbers="true" %}
```rust
use std::rc::{Rc, Weak};
use std::cell::RefCell;

#[derive(Debug)]
struct Node {
    value: i64,
    parent: Option<Weak<RefCell<Node>>>,
    children: Vec<Rc<RefCell<Node>>>,
}

fn main() {
    let mut root = Rc::new(RefCell::new(Node {
        value: 42,
        parent: None,
        children: vec![],
    }));
    let child = Rc::new(RefCell::new(Node {
        value: 43,
        children: vec![],
        parent: Some(Rc::downgrade(&root))
    }));
    root.borrow_mut().children.push(child);

    println!("graph: {root:#?}");
}
```
{% endcode %}

위에 나오는 내용은 코딩에 실질적으로 필요한 참조 관련 내용 전부라고 볼 수 있습니다. 이미 러스트 라이브러리에서 제공된 기능을 활용하여 필요한 기능을 구현합니다.   RefCell이나 Cell을 대체할 무언가를 만들 일은 OS  코딩이 아니라면  없을 듯 합니다.&#x20;

라인 7의  `Weak`는 순환 참조 때문에 C++의 `weak_ptr`과 같은 기능을 합니다.  라인 22의 `borrow_mut()`로 내부 셀의 변경이 가능하도록 `DerefMut<Target = Node>`를 구현한 `DerefMut`를 돌려줘서 쓰기 참조로 접근할 수 있게 합니다.&#x20;

<details>

<summary>발표자 노트</summary>

* Rc의 카운트는 참조가 있는 한 포함된 값이 유효하다는 것을 보장합니다.
* C++의 std::shared\_ptr처럼요.
* 동일한 할당에 대한 포인터를 생성하고 참조 횟수를 증가시키므로 비용이 저렴합니다. 딥 클론을 만들지 않으며 일반적으로 코드에서 성능 문제를 찾을 때 무시할 수 있습니다.
* make\_mut은 필요한 경우 실제로 내부 값을 복제(copy-on-write)하고 변경 가능한 참조를 반환합니다.
* 참조 개수를 확인하려면 Rc::strong\_count를 사용합니다.
* 언급된 다양한 데이터 유형을 비교합니다. Box는 컴파일 타임에 적용되는 변경 가능한/변경 불가능한 빌림을 활성화합니다. RefCell은 런타임에 적용되는 가변/불변 빌림을 성화하고 런타임에 실패하면 패닉을 일으킵니다.
* Rc::downgrade()는 참조 카운트가 약한 객체를 제공하여 적절하게 삭제되는 사이클을 생성합니다(RefCell과 함께 사용할 가능성이 높습니다).

</details>

Cell은 불변 참조라고 하더라도 내부를 변경 가능하게 하고, RefCell은 &와 \&mut를 컴파일러가 점검하듯이 실행 시간에 가변/불변 참조를 검증합니다.&#x20;

이 부분은 여러 번 공부했으나 많이 쓰지 않아 기억에서 자꾸 사라집니다. 실제 적용할 경우에만 기억에 남을 듯 합니다.&#x20;







