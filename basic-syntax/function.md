# 함수

러스트 버전의 [FizzBuzz](https://en.wikipedia.org/wiki/Fizz\_buzz) 함수입니다:

```rust
fn main() {
    print_fizzbuzz_to(20);
}

fn is_divisible(n: u32, divisor: u32) -> bool {
    if divisor == 0 {
        return false;
    }
    n % divisor == 0
}

fn fizzbuzz(n: u32) -> String {
    let fizz = if is_divisible(n, 3) { "fizz" } else { "" };
    let buzz = if is_divisible(n, 5) { "buzz" } else { "" };
    if fizz.is_empty() && buzz.is_empty() {
        return format!("{n}");
    }
    format!("{fizz}{buzz}")
}

fn print_fizzbuzz_to(n: u32) {
    for i in 1..=n {
        println!("{}", fizzbuzz(i));
    }
}
```

<details>

<summary><strong>Speaker Notes</strong></summary>

* `main` 함수에서 그 아래에 구현한 함수를 참조합니다. 전방 선언(foward declaration)이나 헤더 파일을 필요로 하지 않습니다. 이는 C#이나 java와 같습니다.
* 함수의 파라미터들은 타잎이 뒤에 옵니다 (C/C++과 같은 언어의 역순입니다). 그 다음에 반환 타잎이 옵니다.
* 함수 본문의 마지막 표현식(expression)의 값이 반환값이 됩니다. 함수도 expression이기 때문입니다. ; (세미콜론)이 오면 () (void tuple)이 반환값이 됩니다. return 문으로 값을 반환할 수도 있습니다.
* 어떤 함수들은 반환값이 없는데 그럴 때도 단위 타잎인 ()를 반환값으로 갖습니다. 컴파일러가 리턴 타잎이 생략되면 -> ()로 추론합니다.
* 1..=n 이면 n을 포함한다는 뜻입니다.&#x20;

</details>

<details>

<summary>놀미 노트</summary>

* 러스트의 함수는 블록에 가깝습니다. 함수 파라미터들은 이 블록의 지역 변수에 가깝습니다. 반환값은 이 블록의 값 (표현식이므로)에 해당합니다. 대신, 타잎 추론이 어려운 경우들이 많으므로 타잎을 지정하는 정도로만 블록과 차이가 있습니다.

</details>

<details>

<summary>연습</summary>

* 1..=n이나 1..n이 어떻게 동작하는 걸까요? 숫자 타잎에서 범위를 얻는 연산자일까요? 1..n의 타잎이 있을까요? for 문의 일부일까요?

</details>

\
