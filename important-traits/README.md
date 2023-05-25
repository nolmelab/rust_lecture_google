# 중요한 트레이트들 (Important Traits)

러스트 표준 라이브러리에는 다음과 같은 범용 트레잇들이 정의되어 있습니다:

* [`Iterator`](https://doc.rust-lang.org/std/iter/trait.Iterator.html)와 [`IntoIterator`](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html) 트레잇은 `for` 루프에서 사용됩니다.
* [`From`](https://doc.rust-lang.org/std/convert/trait.From.html)과 [`Into`](https://doc.rust-lang.org/std/convert/trait.Into.html) 트레잇은 값을 변환할 때 사용됩니다.
* [`Read`](https://doc.rust-lang.org/std/io/trait.Read.html)와 [`Write`](https://doc.rust-lang.org/std/io/trait.Write.html) 트레잇은 I/O에 사용됩니다.
* [`Add`](https://doc.rust-lang.org/std/ops/trait.Add.html), [`Mul`](https://doc.rust-lang.org/std/ops/trait.Mul.html) 등의 트레잇들은 연산자 오버로딩(overloading)에 사용됩니다.
* [`Drop`](https://doc.rust-lang.org/std/ops/trait.Drop.html) 트레잇은 소멸자 정의에 사용됩니다.
* [`Default`](https://doc.rust-lang.org/std/default/trait.Default.html) 트레잇은 어떤 타입의 기본값 인스턴스를 만들때 사용됩니다.



* [ ] 위 링크들 문서에 맞춰서 수정.
