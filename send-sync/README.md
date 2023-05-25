# Send와 Sync

러스트는 어떻게 해서 스레드 간에 특정 데이터 타입이 공유될 수 있거나, 안된다는 것을 알까요? 정답은 다음 두 트레잇에 있습니다:

* [`Send`](https://doc.rust-lang.org/std/marker/trait.Send.html): `T`가 스레드 간 이동이 안전하다면, `T`의 타입은 `Send`입니다.
* [`Sync`](https://doc.rust-lang.org/std/marker/trait.Sync.html): `&T`가 스레드 간 이동이 안전하다면, `T`의 타입은 `Sync`입니다.

`Send`와 `Sync` 트레잇은 [안전하지 않은 트레잇](https://google.github.io/comprehensive-rust/ko/unsafe/unsafe-traits.html)입니다. 컴파일러는 타입의 요소들이 모두 `Send`와 `Sync` 타입이면 자동으로 이 트레잇들을 적용시켜 줍니다. 물론 여러분 스스로 맞다고 알고 있다면 직접 구현해도 됩니다.

Send와 Sync는 컴파일러와 상호 작용이 많은 unsafe 마커 트레이트들입니다.&#x20;

<details>

<summary>발표자 노트</summary>

* `Sync`와 `Send`는 어떤 타입이 특정한 스레드-안전 속성을 가짐을 나타내는 마커로 생각할 수 있습니다.
* 이 두 트레이트는 제너릭에서 제약 조건을 나타내는 트레이트로 사용될 수도 있습니다.

</details>

