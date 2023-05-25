# Tasks

런타임은 스레드와 유사하지만 리소스 사용량이 훨씬 적은 '작업(Task)'이라는 개념이 있습니다.

태스크에는 실행자(Executor)가 진행을 위해 폴링하는 단일 최상위 퓨처(Future)가 있습니다. 이 Future에는 poll 메서드가 폴링하는 중첩된 Future가 하나 이상 있을 수 있으며, 이는 호출 스택에 느슨하게 대응합니다. 타이머와 I/O 작업의 경주와 같이 여러 하위 Future를 폴링하여 태스크 내에서 동시성을 확보할 수 있습니다.

```rust
use tokio::io::{self, AsyncReadExt, AsyncWriteExt};
use tokio::net::TcpListener;

#[tokio::main]
async fn main() -> io::Result<()> {
    let listener = TcpListener::bind("127.0.0.1:6142").await?;
    println!("listening on port 6142");

    loop {
        let (mut socket, addr) = listener.accept().await?;

        println!("connection from {addr:?}");

        tokio::spawn(async move {
            if let Err(e) = socket.write_all(b"Who are you?\n").await {
                println!("socket error: {e:?}");
                return;
            }

            let mut buf = vec![0; 1024];
            let reply = match socket.read(&mut buf).await {
                Ok(n) => {
                    let name = std::str::from_utf8(&buf[..n]).unwrap().trim();
                    format!("Thanks for dialing in, {name}!\n")
                }
                Err(e) => {
                    println!("socket error: {e:?}");
                    return;
                }
            };

            if let Err(e) = socket.write_all(reply.as_bytes()).await {
                println!("socket error: {e:?}");
            }
        });
    }
}
```

<details>

<summary>발표자 노트</summary>

이 예제를 준비된 src/main.rs에 복사하고 거기에서 실행하세요.

* 학생들에게 몇 개의 클라이언트가 연결된 예제 서버의 상태를 시각화해 보라고 합니다. 어떤 작업(Task)이 존재하나요? 그들의 미래(Future)는 무엇인가요?
* 비동기 블록을 본 것은 이번이 처음입니다. 클로저와 비슷하지만 인수를 받지 않습니다. 반환 값은 비동기 fn과 유사한 Future입니다.
* 비동기 블록을 함수로 리팩터링 하고, ? 를 사용해서 에러 처리를 개선하세요.

[tokio의 비동기 처리 튜토리얼](https://tokio.rs/tokio/tutorial)은 꽤 상세하게 Future / Task / Executor의 동작을 설명하고 있습니다.&#x20;

</details>

