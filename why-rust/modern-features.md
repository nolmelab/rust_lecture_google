# 현대적인 특징 (Modern Features)

러스트는 지난 40년간의 모든 (프로그래밍 언어들의) 경험으로 만들어졌습니다.

## [언어적 특징](https://google.github.io/comprehensive-rust/ko/why-rust/modern.html#%EC%96%B8%EC%96%B4%EC%A0%81-%ED%8A%B9%EC%A7%95) <a href="#undefined" id="undefined"></a>

* 열거형과 패턴 매칭.
* 제네릭.
* FFI 런타임 오버헤드 없음.
  * _역주: FFI: Foreign Function Interface. 타 언어 코드를 호출하기 위한 인터페이스_
* 제로 코스트 추상화.

## [도구들](https://google.github.io/comprehensive-rust/ko/why-rust/modern.html#%EB%8F%84%EA%B5%AC%EB%93%A4) <a href="#undefined" id="undefined"></a>

* 친절한 컴파일러 오류메시지.
* 내장 종속성 관리자.
* 내장 테스트 지원.
* LSP (Language Server Protocol, 언어 서버 프로토콜) 지원이 잘되어 있음.

<details>

<summary>발표자 노트</summary>

* C++ 와 유사하게 제로 코스트 추상화는 CPU나 메모리를 사용하여 상위레벨 프로그래밍 구조를 만드는데 ’비용’을 지불할 필요가 없습니다. 예를 들어 `for` 루프와 `iter().fold()` 구조를 사용하는 것과 거의 동일한 낮은 수준의 명령어가 생성될 것 입니다.
* 러스트의 열거형(enum)은 합계 타입(sum type)으로 알려진 대수학적 데이터형(Algebraic Data Type)으로, 타입 시스템이 `Option<T>`와 `Result<T, E>`등을 표현할 수 있게 해줍니다.
* 오류를 읽어보시기 바랍니다 — 오랜기간 많은 개발자들이 컴파일러 출력을 무시하는데 익숙해져 있습니다. 러스트 컴파일러는 다른 컴파일러보다 더 수다스럽고, 복사-붙여넣기 할 수 있는 정도의 코드 피드백을 제공하는 경우가 많습니다.
*   러스트 표준 라이브러리는 Java, Python이나 Go와 같은 언어에 비해서 규모가 작습니다. 당연히 포함되어야 한다고 생각할 수도 있는 아래와 같은 것들이 러스트의 표준 라이브러리에 없습니다:

    * 난수 생성기, 하지만 [rand](https://docs.rs/rand/)문서를 참조하시기 바랍니다.
    * SSL 또는 TLS지원, 하지만 [rusttls](https://docs.rs/rustls/)문서를 참조하시기 바랍니다.
    * JSON 지원, 하지만 [serde\_json](https://docs.rs/serde\_json/) 문서를 참조하시기 바랍니다. 그 이유는 표준 라이브러리에서 한 번 어떤 기능을 제공하면 뺄 수 없으며, 매우 안정적이어야 하기 때문입니다. 위에 언급한 기능들은 아직 러스트 커뮤니티가 최고의 솔루션을 찾지 못했기 때문에 표준 라이브러리에 포함되지 않았습니다. 어쩌면 이들 중 몇 개는 ’최고의 솔루션’이 아예 존재할 수 없을 지도 모릅니다.

    러스트는 카고라는 패키지 관리자가 내장되어 있고, 서드파티 크레이트를 다운로드, 컴파일 하기 매우 쉽습니다. 이 또한 표준 라이브러리가 작은 이유입니다.

    좋은 서드파티 크레이트를 찾는 것은 어렵습니다. [https://lib.rs](https://lib.rs/) 와 같은 사이트가 신뢰할수 있는 좋은 크레이트를 비교하여 찾는데 좋습니다.
* [rust-analyzer](https://rust-analyzer.github.io/)는 주요 IDE나 텍스트 에디터에서 사용되는 러스트용 LSP서버 입니다.

</details>

<details>

<summary>놀미 노트</summary>

* enum과 패턴 매칭은 매우 강력합니다. trait를 통한 구조화와 조합은 유연성을 유지하면서 큰 시스템을 만들 수 있게 합니다.
* cargo를 쓰면 다른 IDE가 굉장히 불편해집니다. 하나의 프로젝트에서 여러 바이너리, 예제, 테스트를 실행할 수 있습니다. 필요한 패키지도 잘 찾아서 알아서 설치해줍니다.
* 러스트 분석기(rust analyzer)는 추론된 타잎 표시를 깔끔하게 잘 해주고 컴파일 전에 에러를 알려줍니다. 에러 메세지는 컴파일러 에러 메세지와 동일합니다. 많은 분석을 하면서도 상당히 빠르게 반응합니다.

</details>
