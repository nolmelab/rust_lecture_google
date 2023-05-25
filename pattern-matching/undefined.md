# 열거형 분해 (역구조화)

역구조화는 destructuring의 또 다른 번역입니다. 구조 분해 또는 분해가 그 뜻에 맞고 자연스러워 보입니다.&#x20;

구조체나 열거형 값의 일부를 패턴 매치를 통해 변수에 바인딩할 수 있습니다. 간단한 `enum` 타입을 먼저 살펴보겠습니다:

```rust
enum Result {
    Ok(i32),
    Err(String),
}

fn divide_in_two(n: i32) -> Result {
    if n % 2 == 0 {
        Result::Ok(n / 2)
    } else {
        Result::Err(format!("cannot divide {n} into two equal parts"))
    }
}

fn main() {
    let n = 100;
    match divide_in_two(n) {
        Result::Ok(half) => println!("{n} divided in two is {half}"),
        Result::Err(msg) => println!("sorry, an error happened: {msg}"),
    }
}
```

`match`구문에서 `divide_in_two`함수에서 반환되는 `Result` 값을 두 개의 팔에서 _분해(destructure)_ 하였습니다. 첫번째  팔에서 `half`는 `Ok` 분류에 담긴 값으로 바인딩됩니다. 두번째 팔에서 `msg`는 오류 메시지 문자열에 바인딩됩니다.

영문에서는 match arm으로 패턴의 일치 종류에 해당하는 부분을 부릅니다.&#x20;

<details>

<summary>발표자 노트</summary>

* **`[1]`**` ``if`/`else` 표현식은 열거형을 반환하고, 이 값은 나중에 `match`로 분해됩니다.

<!---->

* 열거형에 세번째 variant를 추가하고 코드를 실행하여 오류를 표시해보세요. 코드 어느 부분에 누락이 있는지, 그리고 컴파일러가 어떤 식으로 힌트를 주는지 같이 살펴보세요.

</details>

<details>

<summary>놀미 노트</summary>

**\[1]** if / else가 표현식이라는 점에 유의하세요. 러스트는 표현식이 상당히 많습니다.&#x20;

</details>
