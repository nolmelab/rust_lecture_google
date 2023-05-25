# 열거형 (enum)

`enum` 키워드는 몇 가지 유형(variant)으로 표현되는 타입을 생성합니다:

```rust
fn generate_random_number() -> i32 {
    4  // Chosen by fair dice roll. Guaranteed to be random.
}

#[derive(Debug)]
enum CoinFlip {
    Heads,
    Tails,
}

fn flip_coin() -> CoinFlip {
    let random_number = generate_random_number();
    if random_number % 2 == 0 {
        return CoinFlip::Heads;
    } else {
        return CoinFlip::Tails;
    }
}

fn main() {
    println!("You got: {:?}", flip_coin());
}
```

<details>

<summary>발표자 노트</summary>

키 포인트:

* 열거형은 값들의 집합을 하나의 타입으로 표현할 수 있게 합니다.
* 위의 `CoinFlip` 열거형 타입은 `Heads`와 `Tail` 두가지 variant를 가집니다. 열거형 타입의 variant는 네임스페이스를 붙여서 사용합니다.
* 구조체와 열거형을 비교해 볼까요?
  * 구조체나 열거형 모두, 필드가 하나도 없는 단순한 형태도 가능 하고, 여러 타입의 필드를 가질 수도 있습니다.
  * 둘 다 연관함수를 `impl`블록으로 정의 할 수 있습니다.
  * 열거형 타입의 각 variant를 별도의 구조체로 정의할 수도 있지만, 그러면 열거형을 사용했을 때처럼 하나의 타입으로 취급할 수 없습니다.

</details>

<details>

<summary>놀미 노트</summary>

열거형은 다른 언어에서 볼 수 있는 분류를 위해서 사용할 수 있습니다.&#x20;

다른 언어와 달리 러스트의 열거형은 구현(impl) 블록에서 함수를 추가할 수 있습니다. 또 다른 타잎들을 분류로 포함할 수 있습니다. 이를 대수적 자료 구조라고 하는데 패턴 일치와 함께 러스트에서 **매우 중요한 도구**로 사용합니다.&#x20;

</details>
