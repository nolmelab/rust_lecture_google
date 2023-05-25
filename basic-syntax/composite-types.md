# 복합 타잎 (Composite Types)

배열과 튜플이 있습니다.&#x20;

```rust
fn main() {
    let mut a: [i8; 10] = [42; 10];
    a[5] = 0;
    println!("a: {:?}", a);
}
```

```rust
fn main() {
    let t: (i8, bool) = (7, true);
    println!("1st index: {}", t.0);
    println!("2nd index: {}", t.1);
}
```

초반의 과정 진행이 매우 빠르게 이루어집니다. [Rust by Example ](https://doc.rust-lang.org/rust-by-example/) 예제 위주로 간결하게 설명하므로 이해가 잘 안 되거나 더 보고 싶은 항목이 있으면 이 쪽을 참고합니다. [Rust Lang 문서](https://doc.rust-lang.org/book/)는 설명이 많이 이 과정을 진행하면서 보기에는 좋지 않은 듯 합니다. 그래도 좋은 문서이므로 필요한 항목을 찾아 빠르게 살펴볼 수는 있습니다.&#x20;

<details>

<summary>발표자 노트</summary>

배열:

* 배열은, 같은 타입 `T`의 값이 `N`개 있는 것입니다. 여기서 `N`은 컴파일 타임에 결정된 값이어야 합니다. 이 길이도 타입의 일부입니다. 따라서, `[u8; 3]`와 `[u8; 4]`은 서로 다른 타입입니다.
* 리터럴을 사용하여 배열에 값을 할당할 수 있습니다.
* 포매팅 문자열에서 `?`는 디버깅 출력을 의미합니다. `{}`는 기본 출력이며, `{:?}`는 디버깅 출력입니다. `{a}`, `{a:?}`와 같이 출력할 변수 이름을 포매팅 문자열에 포함시킬 수도 있으며, 이 경우 인자 `a`는 별도의 인자로 추가하지 않습니다.
* `#`을 추가하면(`{a:#?}`) 좀 더 읽기 쉬운 “이쁜” 형태로 출력이 됩니다.

튜플:

* 배열과 마찬가지로 튜플은 고정 길이를 갖습니다.
* 튜플은 서로 다른 타입의 값들을 하나의 복합 타입으로 묶습니다.
* 튜플에 속한 값은 `t.0`, `t.1`과 같이 인덱스로 접근할 수 있습니다.
* 비어있는 튜플`()`은 단위 타입(unit type)이라고도 합니다. 이는 타입이면서 해당 타입의 유일하며 유효한 값입니다. 즉 타입과 값이 모두 `()`입니다. 예를 들어 함수나 식에서 반환 값이 없음을 나타낼 때 사용합니다.
  * 다른 언어에서 익숙한 `void` 개념으로 생각할 수 있습니다

</details>

<details>

<summary>연습</summary>

* [\[Rust By Example : Primitives/Tuples\]](https://doc.rust-lang.org/rust-by-example/primitives/tuples.html)를 카고로 만든 프로젝트에서 vscode나 IDE에서 직접 실행해 봅니다.
* [\[Rust By Example : Primitives/Arraus and Slices\]](https://doc.rust-lang.org/rust-by-example/primitives/array.html)를 카고로 만든 프로젝트에서 vscode나 IDE에서 직접 실행해 봅니다.

슬라이스는 처음에 낯선 부분입니다. 동일 타잎의 연속된 메모리에 대한 조각이라는 의미입니다. 배열과 거의 같으나 컴파일러가 길이를 알 수 없다는 차이가 있습니다. 뒤에서 더 다룹니다.

</details>
