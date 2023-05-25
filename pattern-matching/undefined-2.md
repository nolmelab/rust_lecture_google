# 배열 분해 (역구조화)

배열이나 튜플, 슬라이스도 그 요소들에 대해 패턴 매칭으로 분해할 수 있습니다:

```rust
#[rust#[rustfmt::skip]
fn main() {
    let triple = [0, -2, 3];
    println!("Tell me about {triple:?}");
    match triple {
        [0, y, z] => println!("First is 0, y = {y}, and z = {z}"),
        [1, ..]   => println!("First is 1 and the rest were ignored"),
        _         => println!("All elements were ignored"),
    }
}}
```

길이를 알 수 없는 슬라이스에 대해서도 패턴으로 분해할 수 있습니다.

```rust
fn main() {
    inspect(&[0, -2, 3]);
    inspect(&[0, -2, 3, 4]);
}

#[rustfmt::skip]
fn inspect(slice: &[i32]) {
    println!("Tell me about {slice:?}");
    match slice {
        &[0, y, z] => println!("First is 0, y = {y}, and z = {z}"),
        &[1, ..]   => println!("First is 1 and the rest were ignored"),
        _          => println!("All elements were ignored"),
    }
}
```

<details>

<summary>발표자 노트</summary>

* `_`를 사용하여 요소를 매칭하는 패턴을 추가해보세요.
* 배열에 값을 더 추가해보세요.
* `..`가 요소 개수에 상관없이 매치될 수 있음을 알려주세요.
* **`[1]`**` `` ``[.., b] `나 `[a@.., b]`와 같은 패턴으로 꼬리 부분을 매칭하는 것을 보여주세요.

**\[1]** a @ .. 에서 매칭되는 값들이 a에 할당됩니다.

</details>

\\
