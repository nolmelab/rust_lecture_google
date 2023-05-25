# 틈새 최적화 (Niche Optimization)

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

`Box`는 비어있을 수 없습니다 (Nil이.빈 리스트이므로).   따라서 포인터는 항상 유효하며 `null`이 아닙니다. 이는 컴파일러가 메모리 레이아웃을 최적화 할 수 있게 해줍니다:

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption><p>틈새 최적화로 하나의 필드만 메모리를 가짐</p></figcaption></figure>

enum이 값을 분류해서 가질 수가 있어서 가능해졌다는 점도 알아야 합니다.&#x20;





