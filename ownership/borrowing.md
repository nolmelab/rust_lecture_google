# 빌림 (Borrowing)

함수 호출시 값의 소유권을 이동하는 대신의 함수가 값을 _빌려올 수_ 있습니다:

```rust
#[derive(Debug)]
struct Point(i32, i32);

fn add(p1: &Point, p2: &Point) -> Point {
    Point(p1.0 + p2.0, p1.1 + p2.1)
}

fn main() {
    let p1 = Point(3, 4);
    let p2 = Point(10, 20);
    let p3 = add(&p1, &p2);
    println!("{p1:?} + {p2:?} = {p3:?}");
}
```

* `add` 함수는 두 `Point` 객체 값을 \_빌려\_와서 새로운 `Point` 객체를 반환합니다.
* `p1`과 `p2`의 소유권은 여전히 호출자(`main`함수)에 있습니다.

<details>

<summary> 발표자 노트</summary>

스택에 할당된 값을 리턴하는 것에 대한 참고:

* `add`에서 값을 반환하는 것은 매우 값이 싸다는 것을 설명하세요. 왜냐하면, 컴파일러가 복사 과정을 생략할 수 있기 때문입니다. 위 코드를 스택 주소를 출력하도록 수정하고 [Playground](https://play.rust-lang.org/)에서 수행해 보세요. “디버그” 최적화 레벨에서는 주소가 바뀌지만, “릴리즈” 레벨에서는 바뀌지 않습니다:

```rust
#[derive(Debug)]
struct Point(i32, i32);

fn add(p1: &Point, p2: &Point) -> Point {
    let p = Point(p1.0 + p2.0, p1.1 + p2.1);
    println!("&p.0: {:p}", &p.0);
    p
}

fn main() {
    let p1 = Point(3, 4);
    let p2 = Point(10, 20);
    let p3 = add(&p1, &p2);
    println!("&p3.0: {:p}", &p3.0);
    println!("{p1:?} + {p2:?} = {p3:?}");
}
```

* 러스트 컴파일러는 반환값 최적화(RVO)를 수행할 수 있습니다.
* C++에서 copy elision은 생성자의 부수효과(side effect) 가능성이 있어 언어레벨의 정의가 필요하지만 러스트에서는 문제가 되지 않습니다. 만약 RVO가 불가능하면 러스트는 항상 간단하고 효율적인 `memcpy`복사를 수행할 것입니다.

</details>
