# Vec (벡터)

[`Vec`](https://doc.rust-lang.org/std/vec/struct.Vec.html) 는 힙에 할당된 표준 가변 크기 버퍼입니다:

```rust
fn main() {
    let mut v1 = Vec::new();
    v1.push(42);
    println!("v1: len = {}, capacity = {}", v1.len(), v1.capacity());

    let mut v2 = Vec::with_capacity(v1.len() + 1);
    v2.extend(v1.iter());
    v2.push(9999);
    println!("v2: len = {}, capacity = {}", v2.len(), v2.capacity());

    // Canonical macro to initialize a vector with elements.
    let mut v3 = vec![0, 0, 1, 2, 3, 4];

    // Retain only the even elements.
    v3.retain(|x| x % 2 == 0);
    println!("{v3:?}");

    // Remove consecutive duplicates.
    v3.dedup();
    println!("{v3:?}");
}
```

`Vec`는 러스트에서 안전하게 메모리를 다루는 방법에 대한 보물창고이지만 처음에 보기는 어렵습니다. 응용 프로그램을 중심으로 개별 도메인에 집중하여 연습하면서 차츰 익혀나가면 좋습니다.&#x20;

Vec는 String을 포함하여 많은 곳에서 쓰입니다. 어떤 함수들이 있는지 어떻게 사용하는지 익힐수록 도움이 됩니다.&#x20;

<details>

<summary>발표자 노트</summary>

* `Vec`은 `String`이나 `HashMap`과 같은 컬렉션 타입입니다. 벡터는 데이터를 힙에 저장합니다. 이는 컴파일 시점에 데이터 크기를 알 필요가 없다는 의미고, 런타임에 더 커질 수도 작아질 수도 있습니다.
* `Vec<T>`는 제네릭 타입이기도 합니다. 하지만 `T`를 꼭 지정해줄 필요는 없습니다. 이 경우, 러스트 타입 추론이 벡터에 처음 `push`하는 데이터로 `T`를 알 수 있었습니다.
* `vec![...]`는 `Vec::new()` 대신 쓸 수 있는 표준 매크로로서, 초기 데이터를 추가한 벡터를 생성할 수 있습니다.
* 벡터는 `[` `]`를 사용하여 인덱스로 접근할 수 있습니다. 하지만 범위를 벗어나면 패닉이 발생합니다. 대신 `get`을 사용하면 `Option`을 반환합니다. `pop` 함수는 마지막 요소를 제거합니다.
* 벡터를 순회하면서 값을 변경할 수도 있음을 보여주세요: `for e in &mut v { *e += 50; }`

[벡터 문서](https://doc.rust-lang.org/std/vec/struct.Vec.html)를 보면서 다양한 메서드를 사용해 봅니다.

</details>

