# 실행시 보장되는 것들 (Runtime Guarantees)

런타임 시 정의되지 않음(undefined) 동작 없음:

* 배열 접근시 경계 체크
* 정수형 타입의 변수에서 오버플로우 발생시 동작이 잘 정의되어있습니다.

<details>

<summary>발표자 노트</summary>

* 정수형 오버플로우는 컴파일 타임 플레그를 통해 정의됩니다. 옵션은 패닉(프로그램 크레시) 혹은 올림(wrap-around)입니다. 기본적으로 디버그 모드(`cargo build`)에서는 패닉이, 릴리즈 모드(`cargo build --release`)에서는 wrap-around가 발생합니다.
* 컴파일 플래그를 사용하여 경계체크를 무력화 할 수 없습니다. `unsafe`를 사용하더라도 마찬가지입니다. 하지만 `unsafe`에서 호출 가능한 `slice::get_unchecked`같은 함수는 경계 검사를 수행하지 않습니다.

</details>

<details>

<summary>놀미 노트</summary>

* C++ 같은 언어에서는 Wrap around (넘치면 처음부터 시작)이 기본이고 다른 선택을 제공하지 않습니다. 이런 면이 러스트가 안정성을 많이 고려한 언어라는 점을 잘 보여줍니다.
* 실행시 보장은 라이브러리에서도 다양한 기능을 통해 제공합니다. 과정 후반에 여러 내용들이 나옵니다.

</details>
