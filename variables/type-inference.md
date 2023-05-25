# 타잎 추론 (Type Inference)

러스트는 변수가 어떻게 사용되는지를 보고 그 변수의 타입을 추론합니다:

```rust
fn takes_u32(x: u32) {
    println!("u32: {x}");
}

fn takes_i8(y: i8) {
    println!("i8: {y}");
}

fn main() {
    let x = 10;
    let y = 20;

    takes_u32(x);
    takes_i8(y);
    // takes_u32(y);
}
```

<details>

<summary>발표자 노트</summary>

이 슬라이드는, 러스트 컴파일러가 변수가 어떻게 선언되어 있고, 어떻게 사용되는지를 제약 조건으로 삼아서 변수의 타입을 추론하는 모습을 보여줍니다.

여기서 중요한 것은, 이렇게 명시적인 타입을 생략하고 선언되었다고 해서 “어떤 타입“이라도 다 담을 수 있는 타입이 되는 것은 아니라는 점입니다. 명시적인 타입 선언이 있던 없던, 컴파일러가 생성한 머신코드는 동일합니다. 컴파일러는 단지 타입 선언을 생략할 수 있도록 해서 프로그래머가 더 간결한 코드를 쓸 수 있도록 도와줄 뿐입니다.

아래 코드는, 제네릭 컨테이너를 쓸 때 컨테이터 안에 포함된 데이터의 타입을 명시적으로 쓰지 않고 `_`로 대체하여도 된다는 것을 보여줍니다:

```rust
fn main() {
    let mut v = Vec::new();
    v.push((10, false));
    v.push((20, true));
    println!("v: {v:?}");

    let vv = v.iter().collect::<std::collections::HashSet<_>>();
    println!("vv: {vv:?}");
}
```

[`collect`](https://doc.rust-lang.org/stable/std/iter/trait.Iterator.html#method.collect)는 [`HashSet`](https://doc.rust-lang.org/std/iter/trait.FromIterator.html)을 구현한 `FromIterator`에 의존합니다.

</details>

<details>

<summary>놀미 노트</summary>

* 러스트 분석기(rust analyzer)는 추론된 타잎을 표시해줍니다. auto, var를 사용할 때 타잎을 알 수 없어 불편했던 점을 개선한 기능입니다.

<img src="../.gitbook/assets/image (3) (1).png" alt="" data-size="original">

* FromIterator는 Iterator로부터 해당 타잎을 만들 수 있다는 약속입니다. HashSet, Vec 등의 컬렉션들은 모두 이들 트레이트를 구현하고 있습니다. 트레이트를 통한 약속, 이의 구현에 대해서는 나중에 더 자세히 나옵니다.

</details>
