# Iterators

`Iterator`트레잇을 여러분이 정의한 타입에서 구현해 보겠습니다

```rust
struct Fibonacci {
    curr: u32,
    next: u32,
}

impl Iterator for Fibonacci {
    type Item = u32;

    fn next(&mut self) -> Option<Self::Item> {
        let new_next = self.curr + self.next;
        self.curr = self.next;
        self.next = new_next;
        Some(self.curr)
    }
}

fn main() {
    let fib = Fibonacci { curr: 0, next: 1 };
    for (i, n) in fib.enumerate().take(5) {
        println!("fib({i}): {n}");
    }
}
```

Iterator::take() 메서드는 Iterator를 구현한 Take를 돌려줍니다.&#x20;



<details>

<summary>발표자 노트</summary>

* `Iterator` 트레이트는  컬렉션에 대한 많은 일반적인 함수형 프로그래밍 연산(예: map, filter, reduce 등)을 구현합니다. 이 트레이트는 문서화가 잘  되어 있어 이에 대한 모든 문서를 찾을 수 있습니다. 러스트에서 이러한 함수는 동등한 명령형 구현만큼 효율적인 코드를 생성해야 합니다.
* `IntoIterator`는 루프를 작동시키는 특성입니다. `Vec`와 같은 컬렉션 유형과 `&Vec` 및 `&[T]` 같은 참조가 이를 구현합니다. 범위도 이를 구현합니다. 그렇기 때문에 `for i in some_vec { ... }`에서 벡터를 반복할 수 있지만 `some_vec.next()`가 존재하지 않는 이유입니다.



</details>
