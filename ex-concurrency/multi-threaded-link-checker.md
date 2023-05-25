# 멀티 쓰레드 링크 검사기 (Multi-Threaded Link Checker)

새로 배운것들을 활용해서 멀티 스레드 링크 검사기를 만듭니다. 이 검사기는 웹페이지 안에 있는 링크들이 유효한지 확인합니다. 그리고 재귀적으로 동일 도메인의 다른 모든 페이지가 유효한지 확인합니다.

이를 위해서 [`reqwest`](https://docs.rs/reqwest/)와 같은 HTTP 클라이언트가 필요합니다. 새로운 로컬 프로젝트를 만들고 [`reqwest`](https://docs.rs/reqwest/)를 의존성에 추가하십시요:

```bash
$ cargo new link-checker
$ cd link-checker
$ cargo add --features blocking,rustls-tls reqwest
```

{% hint style="info" %}
만일 `cargo add` 커맨드가 `error: no such subcommand` 로 실패한다면 `Cargo.toml` 파일을 직접 수정해도 됩니다. 아래에 전체 의존성 내용이 있습니
{% endhint %}

링크를 찾기 위해서 [`scraper`](https://docs.rs/scraper/)도 추가합니다:

```bash
$ cargo add scraper
```

마지막으로 오류 처리하는 방법으로 [`thiserror`](https://docs.rs/thiserror/)도 추가합니다:

```bash
$ cargo add thiserror
```

모든 `cargo add`가 끝나면 `Cargo.toml`에 아래 내용이 추가됩니다:

```toml
[package]
name = "link-checker"
version = "0.1.0"
edition = "2021"
publish = false

[dependencies]
reqwest = { version = "0.11.12", features = ["blocking", "rustls-tls"] }
scraper = "0.13.0"
thiserror = "1.0.37"
```

이제 `https://www.google.org/` 같은 웹 페이지를 탐색할 수 있습니다.

`rc/main.rs`파일은 아래와 같습니다:

```rust
use reqwest::blocking::{get, Response};
use reqwest::Url;
use scraper::{Html, Selector};
use thiserror::Error;

#[derive(Error, Debug)]
enum Error {
    #[error("request error: {0}")]
    ReqwestError(#[from] reqwest::Error),
}

fn extract_links(response: Response) -> Result<Vec<Url>, Error> {
    let base_url = response.url().to_owned();
    let document = response.text()?;
    let html = Html::parse_document(&document);
    let selector = Selector::parse("a").unwrap();

    let mut valid_urls = Vec::new();
    for element in html.select(&selector) {
        if let Some(href) = element.value().attr("href") {
            match base_url.join(href) {
                Ok(url) => valid_urls.push(url),
                Err(err) => {
                    println!("On {base_url}: could not parse {href:?}: {err} (ignored)",);
                }
            }
        }
    }

    Ok(valid_urls)
}

fn main() {
    let start_url = Url::parse("https://www.google.org").unwrap();
    let response = get(start_url).unwrap();
    match extract_links(response) {
        Ok(links) => println!("Links: {links:#?}"),
        Err(err) => println!("Could not extract links: {err:#}"),
    }
}
```

아래 커맨드로 소스를 실행합니다

```bash
$ cargo run
```

## [할 일](https://google.github.io/comprehensive-rust/ko/exercises/concurrency/link-checker.html#%ED%95%A0-%EC%9D%BC) <a href="#undefined" id="undefined"></a>

* 스레드를 사용하여 링크를 병렬로 확인합니다: URL을 채널로 보내서 몇 개의 스레드가 URL을 병렬로 체크하도록 합니다.
* `www.google.org`도메인의 모든 페이지를 재귀적으로 확인하기 위해 코드를 확장해서 작성합니다: 차단당하지 않도록 100페이지 정도로 제한을 두시기 바랍니다.
