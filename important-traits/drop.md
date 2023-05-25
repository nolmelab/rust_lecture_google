# Drop

[`Drop`](https://doc.rust-lang.org/std/ops/trait.Drop.html)트레잇을 구현하면, 그 값이 스코프 밖으로 나갈 때 실행될 코드를 작성할 수 있습니다:

```rust
struct Droppable {
    name: &'static str,
}

impl Drop for Droppable {
    fn drop(&mut self) {
        println!("Dropping {}", self.name);
    }
}

fn main() {
    let a = Droppable { name: "a" };
    {
        let b = Droppable { name: "b" };
        {
            let c = Droppable { name: "c" };
            let d = Droppable { name: "d" };
            println!("Exiting block B");
        }
        println!("Exiting block A");
    }
    drop(a);
    println!("Exiting main");
}
```

<details>

<summary>발표자 노트</summary>

* `Drop::drop`은 왜 `self`를 인자로 받지 않습니까?
  * 짧은 대답: 만약 그렇게 된다면 `std::mem::drop`이 블록의 끝에서 호출되고, 다시 `Drop::drop`을 호출하게되 스택 오버플로가 발생합니다.
* `drop(a)`를 `a.drop()`로 변경해 보시기 바랍니다.

</details>
