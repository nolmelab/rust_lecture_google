# 가시성 (Visibility)

모듈의 타입이나 함수는 기본적으로 바깥에 노출되지 않습니다:

* 따라서 모듈의 세부 구현 내용이 감춰집니다.
* 부모와 이웃 항목은 언제나 접근 가능합니다.
* 즉, 모듈 `foo`에서 접근 가능한 항목이라면 `foo` 아래의 모든 모듈에서 접근가능합니다.

```rust
mod outer {
    fn private() {
        println!("outer::private");
    }

    pub fn public() {
        println!("outer::public");
    }

    mod inner {
        fn private() {
            println!("outer::inner::private");
        }

        pub fn public() {
            println!("outer::inner::public");
            super::private();
        }
    }
}

fn main() {
    outer::public();
}
```

<details>

<summary>발표자 노트</summary>

* `pub` 키워드는 모듈에도 사용할 수 있습니다.

또한, 고급 기능으로 `pub(...)` 지정자를 사용하여 공개 범위를 제한할 수 있습니다.

* [공식 문서](https://doc.rust-lang.org/reference/visibility-and-privacy.html#pubin-path-pubcrate-pubsuper-and-pubself)를 참고하세요.
* `pub(crate)`로 가시성을 지정하는 것이 자주 쓰입니다.
* 자주 쓰이진 않지만 특정 경로에 대해서만 가시성을 부여할 수 있습니다.
* 어떤 경우이든 가시성이 부여되면 해당 모듈을 포함하여 하위의 모든 모듈이 적용받습니다.

</details>

```rust
#[macro_use]
#[doc(hidden)]
pub mod macros;

cfg_fs! {
    pub mod fs;
}

mod future;

pub mod io;
pub mod net;

mod loom;

cfg_process! {
    pub mod process;
}

#[cfg(any(
    feature = "fs",
    feature = "io-std",
    feature = "net",
    all(windows, feature = "process"),
))]
mod blocking;
```

tokio의 lib.rs에서 모듈의 가시성을 설정한 한 예시입니다.&#x20;

```rust
mod lookup_host;
pub use lookup_host::lookup_host;

pub mod tcp;
pub use tcp::listener::TcpListener;
pub use tcp::stream::TcpStream;
```

net 모듈에서 다른 모듈을 사용하면서 외부에 선택적으로 노출한 예시입니다.&#x20;
