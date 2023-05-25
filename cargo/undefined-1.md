# 로컬 환경의 카고

만약 개인용 컴퓨터에서 코드를 실행해보려면 먼저 러스트를 설치해야 합니다. [Rust Book](https://doc.rust-lang.org/book/ch01-01-installation.html)의 지침에 따라 `rustc`와 `cargo`를 함께 설치 하시기 바랍니다. 설치 후 아래 커맨드를 통해 각 툴의 버전을 확인 할 수 있습니다:

```shell
% rustc --version
rustc 1.61.0 (fe5b13d68 2022-05-18)
% cargo --version
cargo 1.61.0 (a028ae4 2022-04-29)
```

정상적으로 설치가 되었으면 강의의 코드 블록중 하나를 아래 단계를 따라 로컬에서 실행할 수 있습니다:

1. 예시 블록에 있는 “Copy to clipboard” 버튼을 클릭해서 복사합니다.
2.  터미널에서 `cargo new exercise`를 입력해서 새로운 `exercise/` 폴더를 만듭니다:

    ```shell
    $ cargo new exercise
         Created binary (application) `exercise` package
    ```
3.  `exercise/` 폴더로 이동한 후, `cargo run` 커맨드로 코드를 실행합니다:

    ```shell
    $ cd exercise
    $ cargo run
       Compiling exercise v0.1.0 (/home/mgeisler/tmp/exercise)
        Finished dev [unoptimized + debuginfo] target(s) in 0.75s
         Running `target/debug/exercise`
    Hello, world!
    ```
4.  `src/main.rs`에 코드를 작성합니다. 예를 들어 이전 페이지의 소스를 아래와 같이 `src/main.rs`에 작성합니다

    ```rust
    fn main() {    println!("Edit me!");}
    ```
5.  `cargo run`커맨드로 소스를 빌드하고 실행합니다:

    ```shell
    $ cargo run
       Compiling exercise v0.1.0 (/home/mgeisler/tmp/exercise)
        Finished dev [unoptimized + debuginfo] target(s) in 0.24s
         Running `target/debug/exercise`
    Edit me!
    ```
6. `cargo check`커맨드는 빠르게 에러를 확인할 수 있습니다. `cargo build`는 실행없이 컴파일만 합니다. 이 경우에 `target/debug/`폴더에서 output을 확인 할 수 있습니다. `cargo build --release`커맨드는 릴리즈 버전용 최적화를 켜서 컴파일하며 `target/release/`폴더에서 확인 할 수 있습니다.
7. `Cargo.toml`파일에는 의존성 패키지를 추가할 수 있습니다. `cargo`커맨드를 실행하면 자동으로 의존성 패키지를 다운로드하고 컴파일 까지 해 줍니다.

<details>

<summary>발표자 노트</summary>

수강생들이 카고를 설치하고 로컬 편집기를 이용하도록 독려하세요. 조금 귀찮을 수도 있지만, 이렇게 해야만 좀 더 **실제와 가까운 개발환경**을 갖추게 되는 것입니다.

</details>
