# Default

[`Default`](https://doc.rust-lang.org/std/default/trait.Default.html) 트레잇은 기본 값을 제공합니다.

```rust
#[derive(Debug, Default)]
struct Derived {
    x: u32,
    y: String,
    z: Implemented,
}

#[derive(Debug)]
struct Implemented(String);

impl Default for Implemented {
    fn default() -> Self {
        Self("John Smith".into())
    }
}

fn main() {
    let default_struct: Derived = Default::default();
    println!("{default_struct:#?}");

    let almost_default_struct = Derived {
        y: "Y is set!".into(),
        ..Default::default()
    };
    println!("{almost_default_struct:#?}");

    let nothing: Option<Derived> = None;
    println!("{:#?}", nothing.unwrap_or_default());
}
```

Default 트레이트는 core 라이브러리에 있습니다. core는 컴파일러와 상호 작용하는 트레이트들이 많이 있습니다. 러스트는 이와 같이 라이브러리의 타잎들과 컴파일러가 연동된다는 점에서 특이합니다. 처음에는 이해하기 어려운데 점점 익숙해집니다.&#x20;

<details>

<summary>발표자 노트</summary>

* 트레잇을 직접 구현하거나 `#[derive(Default)]`를 붙여서 컴파일러에게 구현을 맡길 수 있습니다.
* 컴파일러가 제공하는 자동 구현의 경우 모든 필드에 대해 기본 값을 설정한 새 인스턴스를 반환합니다.
  * 구조체의 각 필드 타입들이 모두 `Default`를 구현해야 함을 의미합니다.
* 러스트 표준 타입들은 대부분 `Default`를 구현하고 있으며, 기본 값은 `0`이나 `""`처럼 예상 가능한 값들입니다.
* 구조체 부분 복사를 할때 `default`를 편리하게 사용할 수 있습니다.
* 러스트 표준 라이브러리는 `Default` 트레잇을 구현한 타입을 위한 편의 메서드를 제공하기도 합니다.

</details>
