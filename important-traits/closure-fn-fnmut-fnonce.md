# Closure : Fn, FnMut, FnOnce

클로저 혹은 람다표현식은 익명타입입니다. 이들은 [`Fn`](https://doc.rust-lang.org/std/ops/trait.Fn.html),[`FnMut`](https://doc.rust-lang.org/std/ops/trait.FnMut.html), [`FnOnce`](https://doc.rust-lang.org/std/ops/trait.FnOnce.html) 라는 특별한 트레잇을 구현합니다:

```rust
fn apply_with_log(func: impl FnOnce(i32) -> i32, input: i32) -> i32 {
    println!("Calling function on {input}");
    func(input)
}

fn main() {
    let add_3 = |x| x + 3;
    let mul_5 = |x| x * 5;

    println!("add_3: {}", apply_with_log(add_3, 10));
    println!("mul_5: {}", apply_with_log(mul_5, 20));
}
```

위에 있는 FnMut의 문서 링크에서 실제 정의를 한번 보면 더 이해가 수월합니다.&#x20;

```rust
pub trait FnMut<Args>: FnOnce<Args>
where
    Args: Tuple,
{
    // Required method
    extern "rust-call" fn call_mut(
        &mut self,
        args: Args
    ) -> Self::Output;
}
```

`call_mut()`의 호출은 위의 `func()`처럼 하면 불립니다. `&mut self`는 캡처된 환경 전체로 생각할 수 있을 듯 합니다. 정확한 뜻은 무엇일까요?

<details>

<summary>발표자 노트</summary>

`FnOnce`는 한번만 호출되며 캡처된 값을 소모합니다.

`FnMut`는 캡처된 값을 변경할 수 있으므로 여러번 호출은 가능하지만 동시에 호출 할 수는 없습니다.

`Fn`은 캡처된 값을 소모도 변경도 하지 않고, 혹은 어떤 것도 캡쳐하지 않았을 수도 있기 때문에 동시에 여러번 호출할 수 있습니다.

`FnMut` 는 `FnOnce`의 하위타입입니다. `Fn`은 `FnMut`과 `FnOnce`의 하위 타입입니다. 즉, `FnMut`는 `FnOnce`가 호출되는 곳이면 어디서나 사용 할 수 있고 `Fn`은 `FnMut`와 `FnOnce`가 호출되는 곳이면 어디든 사용할 수 있습니다.

클로저가 `move`와 함께 선언되었다면 그 클로저는 오직 `FnOnce`만 구현합니다.

</details>
