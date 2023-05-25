# 스택 메모리 (Stack)

`String` 타입은 고정 크기 데이터(_역주_: 문자열의 길이, 문자열이 저장된 버퍼의 주소 등)는 스택에 저장하고, 가변 크기 데이터(_역주_: 문자열 버퍼)는 힙에 저장합니다:

```rust
fn main() {
    let s1 = String::from("Hello");
}
```

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

<details>

<summary>발표자 노트</summary>

* 문자열(`String`)은 실제로는 `Vec`입니다. 크기(capacity)와 현재 길이(length) 정보를 가지며, 더 큰 크기가 필요할 경우 힙에서 재 할당을 합니다.
* 힙은 기본적으로 [System Allocator](https://doc.rust-lang.org/std/alloc/struct.System.html)를 통해 할당됩니다. 그리고 [Allocator API](https://doc.rust-lang.org/std/alloc/index.html)를 이용해서 커스텀 메모리 할당자를 만들 수도 있습니다.
* `unsafe` 코드로 메모리 레이아웃을 살펴볼 수 있습니다. 물론 이 코드가 안전하지 않다는 점을 알려주세요!

```rust
fn main() {
    let mut s1 = String::from("Hello");
    s1.push(' ');
    s1.push_str("world");
    // DON'T DO THIS AT HOME! For educational purposes only.
    // String provides no guarantees about its layout, so this could lead to
    // undefined behavior.
    unsafe {
        let (capacity, ptr, len): (usize, usize, usize) = std::mem::transmute(s1);
        println!("ptr = {ptr:#x}, len = {len}, capacity = {capacity}");
    }
}
```

</details>

<details>

<summary>놀미 노트</summary>

* transmute는 C++의 reinterpret\_cast만큼 강력하게 비트 단위 타잎 변환을 해줍니다. 변환 하고자 하는 타잎과 크기만 같다면 변환이 됩니다. String의 transmute 결과가 (capacity, ptr, len)이 되는 건 이해가 아직 잘 안 되는 면이 있습니다.

</details>
