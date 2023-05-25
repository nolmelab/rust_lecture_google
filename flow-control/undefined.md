# 블록

러스트에서 블록은 값과 타입을 갖습니다. 블록의 마지막 표현식이 블록의 값이 됩니다:

{% code lineNumbers="true" %}
```rust
fn main() {
    let x = {
        let y = 10;
        println!("y: {y}");
        let z = {
            let w = {
                3 + 4
            };
            println!("w: {w}");
            y * w
        };
        println!("z: {z}");
        z - y
    };
    println!("x: {x}");
}
```
{% endcode %}

라인 2처럼 블럭의 값을 변수에 지정할 수 있는 기능은 편리합니다. C/C++이라면 함수로 분리해야 가능한 표현입니다.&#x20;

함수에도 동일한 규칙이 적용됩니다. 함수 바디를 이루는 블록의 값이 반환값이 됩니다:

```rust
fn double(x: i32) -> i32 {
    x + x
}

fn main() {
    println!("doubled: {}", double(7));
}
```

위의 `main` 함수는 마지막 표현식이 `;`로 끝나기 때문에 반환되는 값과 타입이 `()`입니다.

<details>

<summary>발표자 노트</summary>

* 러스트에서는 블록이 타입과 값을 가진다는 점이 이 슬라이드의 핵심입니다.
* 블록 마지막 줄을 수정하면서 블록의 값이 어떻게 바뀌는지 보여주세요. 예를 들어, 세미콜론을 넣거나 뺀다든지, 아니면 `return`을 사용해 보세요.

</details>
