# 오류에 상황 정보 추가

[anyhow](https://docs.rs/anyhow/) 크레이트는 에러에 에러가 발생한 문맥에 대한 정보를 추가하기 위해 널리 사용되며, 이를 이용하면 서로 다른 문맥을 나타내기 사용자 정의 오류 타입을 많이 만들어야 하는 불편함을 피할 수 있습니다.

```rust
use std::{fs, io};
use std::io::Read;
use anyhow::{Context, Result, bail};

fn read_username(path: &str) -> Result<String> {
    let mut username = String::with_capacity(100);
    fs::File::open(path)
        .with_context(|| format!("Failed to open {path}"))?
        .read_to_string(&mut username)
        .context("Failed to read")?;
    if username.is_empty() {
        bail!("Found no username in {path}");
    }
    Ok(username)
}

fn main() {
    //fs::write("config.dat", "").unwrap();
    match read_username("config.dat") {
        Ok(username) => println!("Username: {username}"),
        Err(err)     => println!("Error: {err:?}"),
    }
}
```

<details>

<summary>발표자 노트</summary>

* `anyhow::Result<V>`는 `Result<V, anyhow::Error>`의 타입 앨리어스(alias)입니다.
* `anyhow::Error`는 `Box<dyn Error>`의 래퍼 타입이라 할 수 있습니다. 따라서 라이브러리의 공개 API로서 사용하기에 부적합하다고 할 수 있지만 많은 애플리케이션에 널리 사용되고 있습니다.
* 필요하다면 `anyhow::Error`에 저장된 진짜 에러 타입을 꺼내어 검사할 수도 있습니다.
* `anyhow::Result<T>`가 제공하는 기능들이 Go 언어 개발자들에게는 익숙할 것입니다. Go언어에서 반환 값으로 사용하는 `(T, error)` 패턴과 비슷하기 때문입니다.

</details>
