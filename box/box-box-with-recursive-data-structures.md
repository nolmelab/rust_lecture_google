# 재귀자료 구조에서의 Box (Box with Recursive Data Structures)

재귀 데이터나 동적크기의 데이터 타입은 `Box`타입을 사용해야 합니다:

```rust
#[derive(Debug)]
enum List<T> {
    Cons(T, Box<List<T>>),
    Nil,
}

fn main() {
    let list: List<i32> = List::Cons(1, Box::new(List::Cons(2, Box::new(List::Nil))));
    println!("{list:?}");
}
```

<figure><img src="../.gitbook/assets/image (1) (1).png" alt=""><figcaption><p>List::Cons 연결</p></figcaption></figure>

<details>

<summary>발표자 노트</summary>

* 만일 `Box`를 사용하지 않고 `List`에 직접 `List`를 포함하려고 시도한다면, 컴파일러는 구조체의 고정 크기를 계산할 수 없습니다. 컴파일러가 보기에 무한대의 크기로 보일 것입니다.
* `Box`는 일반 포인터와 크기가 같기 때문에 크기를 계산하는 데 문제가 없습니다. 다만 힙에 위치한 `List`의 다음 요소를 가리킬 뿐입니다.
* `List` 정의에서 `Box`를 제거하면 어떤 컴파일러 에러가 나오는지 같이 살펴보세요. “Recursive with indirection”라는 메시지를 보면, 값을 직접 저장하는 대신 `Box`나 비슷한 다른 종류의 참조 타입이 필요하다는 힌트를 얻을 수 있습니다.

</details>

```rust
error[E0072]: recursive type `List` has infinite size
 --> src\main.rs:8:5
  |
8 |     enum List<T> {
  |     ^^^^^^^^^^^^ recursive type has infinite size
9 |         Cons(T, List<T>),
  |                 ------- recursive without indirection
  |
help: insert some indirection (e.g., a `Box`, `Rc`, or `&`) to make `List` representable
  |
9 |         Cons(T, Box<List<T>>),
  |                 ++++       +

For more information about this error, try `rustc --explain E0072`.
```

답까지 친절하게 알려줍니다. C/C++이라면 `List<T>*`를 사용하여 다음 리스트 연결을 관리할 수 있습니다. 여기에 `shard_ptr`이나 `unique_ptr`을 쓰지는 않을 듯 합니다. 러스트는 `Box`나 `Rc`나 `&`(참조로 포인터에 해당) 사용하고 `Box`가 자연스러운 선택으로 보입니다.&#x20;
