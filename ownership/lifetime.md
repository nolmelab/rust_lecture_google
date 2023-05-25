# 수명

빌려온 값은 _수명_을 갖습니다:

* 수명은 생략할 수 있습니다: `add(p1: &Point, p2: &Point) -> Point`.
* 물론 명시할 수도 있습니다: `&'a Point`, `&'document str`.
* `&'a Point` 는 `Point`의 수명이 최소한 `'a`라는 수명보다는 같거나 더 길다는 것을 의미합니다.
* 수명은 항상 컴파일러가 자동으로 추론합니다. 직접 수명을 지정할 수는 없습니다.
  * 수명 표기(`'`)은 수명 추론시 제약조건이 됩니다. 컴파일러는 이 제약조건을 만족시키는 유효한 수명을 만족할 수 있는지 검사를 합니다.



<details>

<summary>연습</summary>

* [Rust by Example의 수명 생략 예제](https://doc.rust-lang.org/rust-by-example/scope/lifetime/elision.html)를 살펴보세요.&#x20;

</details>
