# loop 표현식

마지막으로 무한 루프를 생성하는 루프 키워드가 있습니다.

이 예제에서는 루프를 중단하거나 돌아가서 루프를 중지해야 합니다:

```rust
fn main() {
    let mut x = 10;
    loop {
        x = if x % 2 == 0 {
            x / 2
        } else {
            3 * x + 1
        };
        if x == 1 {
            break;
        }
    }
    println!("Final x: {x}");
}
```

<details>

<summary>발표자 노트</summary>

* **\[1]** break 할 때 값을 줄 수 있습니다.&#x20;
* **\[2]** 루프는 사소하지 않은 값을 반환하는 유일한 루프 구조체라는 점에 유의하세요. 이는 while 및 for 루프와 달리 적어도 한 번은 입력이 보장되기 때문입니다.

</details>

<details>

<summary>놀미 노트</summary>

**\[1]** return 문처럼 값을 돌려줍니다.

```rust
let (mut a, mut b) = (1, 1);
let result = loop {
    if b > 10 {
        break b;
    }
    let c = a + b;
    a = b;
    b = c;
};
// first number in Fibonacci sequence over 10:
assert_eq!(result, 13);
```

`break b;` 에 세미콜론이 리턴문처럼 있습니다.

**\[2]** 사소하지 않은 값을 반환한다는 뜻은 함수처럼 항상 값을 반환하는 블록이 될 수 있다는 뜻으로 보입니다.

</details>

