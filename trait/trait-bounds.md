# 제네릭 타잎 제한 (Trait Bounds)

제네릭을 이용하다 보면 타입이 어떤 트레잇을 구현하고 있어야 하는 경우가 있습니다. 그래야 그 트레잇의 메서드를 호출할 수 있기 때문입니다.

여기서 Bounds는 Bound 된 것들로 해석되어야 할 것 같습니다. 제네릭에 붙어있는 트레이트들 또는 만족해야 하는 트레이트들로 이해할 수 있습니다. C#의 where 문에서 타잎을 제한할 수 있는 기능이나 C++의 Concept과 유사한 기능입니다.&#x20;

`T: Trait` 혹은 `impl Trait`를 사용하면 됩니다:

```rust
fn duplicate<T: Clone>(a: T) -> (T, T) {
    (a.clone(), a.clone())
}

// Syntactic sugar for:
//   fn add_42_millions<T: Into<i32>>(x: T) -> i32 {
fn add_42_millions(x: impl Into<i32>) -> i32 {
    x.into() + 42_000_000
}

// struct NotClonable;

fn main() {
    let foo = String::from("foo");
    let pair = duplicate(foo);
    println!("{pair:?}");

    let many = add_42_millions(42_i8);
    println!("{many}");
    let many_more = add_42_millions(10_000_000);
    println!("{many_more}");
}
```

러스트가 빠르게 발전하고 여러 시도가 있다보니 experimental 기능도 많고 편의 기능으로 여러 기능이 추가되는 경우도 많습니다. T : Bounds, impl Bounds, where Bounds와 같이 세 가지 선택할 수 있는 방법이 있습니다. 아래는 where를 사용한 예시입니다.&#x20;

```rust
pub fn retain<F>(&mut self, mut f: F)
where
    F: FnMut(&T) -> bool,
{
    self.retain_mut(|elem| f(elem));
}
```

<details>

<summary>발표자 노트</summary>

`where` 문법을 사용할 수도 있습니다. 수강생들도 코드를 읽다가 그 문법을 마주할 수 있습니다.

```rust
fn duplicate<T>(a: T) -> (T, T)
where
    T: Clone,
{
    (a.clone(), a.clone())
}
```

* 이를 이용하면 타입 파라메터가 많은 경우 함수 시그니처를 간결하게 정리하는 데 도움이 됩니다.
* 좀 더 강력한 추가 기능도 제공합니다.
  * `:` 왼쪽에 임의의 타입(예를 들어 `Option<T>`)을 사용할 수 있습니다.

</details>

