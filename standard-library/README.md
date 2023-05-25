# 표준 라이브러리 (standard library)

러스트에서 제공하는 표준 라이브러리는 러스트로 라이브러리나 프로그램을 작성할 때 공통적으로 사용할 수 있는 여러 타입들을 포함하고 있습니다. 이를 통해 서로 다른 두 라이브러리라 하더라도 함께 사용하는데 큰 어려움이 없게 됩니다. 예를 들면 두 라이브러리 모두 같은 `String` 타입을 사용하기 때문입니다.

일반적인 타입은 아래와 같습니다:

* [`Option`과 `Result`](https://google.github.io/comprehensive-rust/ko/std/option-result.html) : 어떤 값이 있거나 없거나 하는 경우, 그리고 [오류 처리](https://google.github.io/comprehensive-rust/ko/error-handling.html)에 사용합니다.
* [`String`](https://google.github.io/comprehensive-rust/ko/std/string.html): 기본적인 문자열 타입으로, 문자열 데이터를 소유하는 경우에 사용합니다.
* [`Vec`](https://google.github.io/comprehensive-rust/ko/std/vec.html): 가변 크기의 표준 벡터 타입입니다.
* [`HashMap`](https://google.github.io/comprehensive-rust/ko/std/hashmap.html): 해시 알고리즘을 따로 지정할 수도 있는 해시맵 타입입니다.
* [`Box`](https://google.github.io/comprehensive-rust/ko/std/box.html): 힙 데이터에 대한 소유 포인터입니다.
* [`Rc`](https://google.github.io/comprehensive-rust/ko/std/rc.html): 힙에 할당된 데이터에 대한 참조 카운팅 공유 포인터입니다.

<details>

<summary>발표자 노트</summary>

* 사실, 러스트의 표준 라이브러리는 `core`, `alloc`, `std`와 같이 계층(layer)으로 나눠집니다.
* **`[1]`**` ``core`는 `libc`나 할당자(allocator), 심지어 OS에도 의존하지 않는 가장 기본적인 함수와 타입을 포함합니다.
* `alloc`은 `Vec`, `Box`, `Arc`와 같이 전역 힙 할당이 필요한 타입을 포함합니다.
* 임베디드 러스트 응용프로그램은 주로 `core`만 사용하거나 가끔 `alloc`을 함께 사용합니다

**\[1]** `core` 라이브러리는 다시 `std`에서 사용가능하게 만듭니다. 예를 들어, `std::ptr`은 `core::ptr`입니다.

</details>
