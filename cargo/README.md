# 카고(Cargo) 사용하기

러스트를 시작하려고하면 당신은 곧 [Cargo](https://doc.rust-lang.org/cargo/)라는, 러스트 생태계에서 사용하는 표준 빌드/실행 도구를 만날 것 입니다. 여기서는 카고가 무엇인지, 그리고 카고가 러스트 생태계에서 어떤 역할을 하는지, 그리고 이 강의에서 어떻게 사용될 지에 대해 간략히 설명하겠습니다.

## [설치하기](https://google.github.io/comprehensive-rust/ko/cargo.html#%EC%84%A4%EC%B9%98%ED%95%98%EA%B8%B0) <a href="#undefined" id="undefined"></a>

[**Rustup (추천)**](https://google.github.io/comprehensive-rust/ko/cargo.html#rustup-%EC%B6%94%EC%B2%9C)

러스트 재단에서 관리하고 있는 [rustup](https://rustup.rs/) 도구를 사용하여 카고 및 러스트 컴파일러 등 표준 도구를 설치 할 수 있습니다.

카고(cargo)와 러스트 컴파일러(rustc)와 함께, rustup은 툴체인을 설치하고, 다른 툴체인으로 전환하고, 크로스 컴파일 설정을 하는 일을 담당하는 커맨드 라인 유틸리티 입니다.

#### [패키지 매니저](https://google.github.io/comprehensive-rust/ko/cargo.html#%ED%8C%A8%ED%82%A4%EC%A7%80-%EB%A7%A4%EB%8B%88%EC%A0%80) <a href="#undefined" id="undefined"></a>

[**데비안**](https://google.github.io/comprehensive-rust/ko/cargo.html#%EB%8D%B0%EB%B9%84%EC%95%88)

데비안이나 우분투에서 cargo, 러스트 소스코드, [러스트 포매터](https://github.com/rust-lang/rustfmt)를 아래 커맨드로 설치합니다.

```shell
$ sudo apt install cargo rust-src rustfmt
```

이렇게 하면 [러스트 분석기(rust-analyzer)](https://rust-analyzer.github.io/)를 이용해서 특정 심볼이 정의된 위치로 쉽게 이동할 수 있습니다. 우리는 에디터로 [VS Code](https://code.visualstudio.com/)를 추천합니다만, 사실 LSP([Language Server Protocol](https://microsoft.github.io/language-server-protocol/overviews/lsp/overview/))를 지원한다면 어떤 에디터도 무방합니다.

어떤 사람들은 [JetBrains](https://www.jetbrains.com/clion/) 제품군을 선호하기도 합니다. 이 제품들은 rust-analyzer 를 활용하지 않고 IDE 자체적으로 구문분석을 합니다. 만약 이 IDE를 설치하셨다면 [Rust Plugin](https://www.jetbrains.com/rust/)를 설치하시기 바랍니다. 다만 2023년 1월 기준, 디버깅은 JetBrains IDEA suite의 CLion 버전에서만 작동한다는 점에 유의하시기 바랍니다.

<details>

<summary>놀미 노트</summary>

* 러스트 분석기는 필수적입니다. 러스트 분석기 없이 러스트로 코딩하면 러스트가 매우 불편한 언어라는 인상을 갖게 되므로 꼭 러스트 분석기가 지원되는 환경에서 시작해야 합니다.

</details>
