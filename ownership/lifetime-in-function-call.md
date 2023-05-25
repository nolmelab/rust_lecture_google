# 함수 호출에서의 수명

함수는 인수를 빌리는 것 외에도 빌린 값을 반환할 수 있습니다:

```rust
#[derive(Debug)]
struct Point(i32, i32);

fn left_most<'a>(p1: &'a Point, p2: &'a Point) -> &'a Point {
    if p1.0 < p2.0 { p1 } else { p2 }
}

fn main() {
    let p1: Point = Point(10, 10);
    let p2: Point = Point(20, 20);
    let p3: &Point = left_most(&p1, &p2);
    println!("left-most point: {:?}", p3);
}
```

* `'a`는 제네릭 매개변수로 컴파일러로에 의해 추론됩니다.
* 수명의 이름은 `'` 로 시작하며 보통 `'a`를 많이 씁니다.
* `&'a Point` 는 `Point`의 수명이 `'a` 수명과 최소한 같거나 더 길다는 것을 의미합니다.
  * 매개변수들이 서로 다른 범위에 있을 경우 “최소한“이라는 조건이 중요합니다.

<details>

<summary>발표자 노트</summary>

위의 예시에서 다음을 시도해 보시기 바랍니다:

* `p2`와 `p3`를 새로운 범위(`{...}`)로 아래 코드와 같이 이동해 봅니다:

```rust
#[derive(Debug)]
struct Point(i32, i32);

fn left_most<'a>(p1: &'a Point, p2: &'a Point) -> &'a Point {
    if p1.0 < p2.0 { p1 } else { p2 }
}

fn main() {
    let p1: Point = Point(10, 10);
    let p3: &Point;
    {
        let p2: Point = Point(20, 20);
        p3 = left_most(&p1, &p2);
    }
    println!("left-most point: {:?}", p3);
}
```

* `p3`의 수명이 `p2` 보다 길기 때문에 이 예제는 컴파일되지 않음을 확인하시기 바랍니다.
* 작업공간을 초기화 한 후 함수 시그니처를 `fn left_most<'a, 'b>(p1: &'a Point, p2: &'a Point) -> &'b Point`로 변경해 봅니다. 이 경우 `'a`와 `'b`사이의 관계가 불분명하기 때문에 컴파일 되지 않습니다.
* 이 에러를 설명하는 또 다른 방법은 다음과 같습니다:
  * 이 함수는 두 값을 빌려서, 새로운 참조를 반환합니다.
  * 이 반환된 참조는 두 입력 중 하나로 부터 와야 합니다. (아니면 전역 변수로 부터)
  * 두 입력 중 어떤 것일까요? 컴파일러는 이를 알아야 합니다. 그래야만 함수 호출부에서 봤을 때, 반환된 참조의 수명이 원래 값을 수명보다 길지 않음을 확인할 수 있기 때문입니다.

</details>
