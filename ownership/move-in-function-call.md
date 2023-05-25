# 함수 호출에서 이동

값을 함수에 전달할때, 그 값은 매개변수에 할당됩니다. 이때 소유권의 이동이 일어납니다:

```rust
fn say_hello(name: String) {
    println!("Hello {name}")
}

fn main() {
    let name = String::from("Alice");
    say_hello(name);
    // say_hello(name);
}
```

<details>

<summary>발표자 노트</summary>

* `say_hello`함수의 첫번째 호출시 `main`함수는 자신이 가진 `name`에 대한 소유권을 포기하므로, 이후 `main` 함수에서는 `name`을 사용할 수 없습니다.
* `name`에 할당된 힙 메모리는 `say_hello`함수의 끝에서 해제됩니다.
* `main`함수에서 `name`을 참조로 전달(빌림)하고(`&name`), `say_hello`에서 매개변수를 참조형으로 수정한다면 `main`함수는 `name`의 소유권을 유지할 수 있습니다.
* 또는 첫번째 호출 시 `main`함수에서 `name`을 복제하여 전달할 수도 있습니다.(`name.clone()`)
* 러스트는 이동을 기본으로 하고 복제를 명시적으로 선언하도록 만듬으로, 의도치 않게 복사본을 만드는 것이 C++에서보다 어렵습니다.

</details>

<details>

<summary>놀미 노트</summary>

* 함수의 아규먼트는 함수 블록 내에 선언된 스택 변수처럼 동작합니다. 따라서, 이동이 되는 건 매우 자연스러운 동작입니다.

</details>
