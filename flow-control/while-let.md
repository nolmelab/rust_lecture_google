# while let 반복문

`if let`과 마찬가지로 패턴에 대해 값을 반복적으로 테스트하는 `while let` 변형이 있습니다:

```rust
fn main() {
    let v = vec![10, 20, 30];
    let mut iter = v.into_iter();

    while let Some(x) = iter.next() {
        println!("x: {x}");
    }
}
```

`v.into_iter()`가 반환한 반복자는 `next()`가 호출될 때마다 `Option<i32>`를 반환합니다. 반복자가 완료될 때까지는 `Some(x)`를 반환하고 마지막엔 `None`을 반환합니다. `while let`을 통해 반복자의 모든 아이템을 확인할 수 있습니다.

Vec::into\_iter()는 IntoIter 트레이트를 구현한 함수입니다. into는 보통 훔쳐서 이동시킬 때 쓰는 단어이고 여기서도 리시버(수진자)가 self인 into\_iter() 함수이기 때문에 Vec가 이동됩니다.&#x20;

다른 언어 C/C++ 등에서 while 문으로 iterator를 순회할 때 코드와  한번 비교해보세요.

<details>

<summary>발표자 노트</summary>

* `while let`은 값이 패턴에 매치되는 동안 계속됩니다.
* `while let` 루프 대신 무한 루프를 사용하고 `iter.next()`가 빈 값을 반환할 때 루프를 빠져나오도록 작성할수도 있습니다. `while let`은 그러한 경우를 위한 문법적 편의를 제공합니다.

</details>

