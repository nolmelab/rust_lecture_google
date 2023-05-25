# 경로 (path)

경로는 아래와 같이 구분합니다:

1. 상대 경로
   * `foo` 또는 `self::foo`는 현재 모듈 내부의 `foo`를 가리킵니다.
   * `super::foo`는 부모 모듈의 `foo`를 가리킵니다.
2. 절대 경로
   * `crate::foo`는 현재 크레이트 루트의 `foo`를 가리킵니다.
   * `bar::foo`는 `bar`크레이트의 `foo`를 가리킵니다.



모듈은 사용 시 다른 모듈의 심볼을 범위에 가져올 수 있습니다. 일반적으로 각 모듈의 상단에 다음과 같은 내용이 표시됩니다.

```rust
use std::collections::HashSet;
use std::mem::transmute;
```

```rust
use tokio::net::{TcpListener, TcpStream};
use tokio::sync::{mpsc, Mutex};
use tokio_stream::StreamExt;
use tokio_util::codec::{Framed, LinesCodec};

use futures::SinkExt;
use std::collections::HashMap;
use std::env;
use std::error::Error;
use std::io;
use std::net::SocketAddr;
use std::sync::Arc;
```

tokio의 examples/chat.rs에서 use로 다른 모듈들에서 가져온 예입니다.&#x20;

self, super가 없으면 절대 경로의 모듈로 생각할 수 있습니다. `use tokio::sync::mpsc` 에서 tokio 패키지부터 시작하는 모듈의  mpsc모듈임을 알 수 있습니다. 모듈의 이름 규약이 스네이크 케이스를 사용하기 때문에 모듈이라고 알 수 있습니다.&#x20;

[명명 규칙](https://rust-lang.github.io/api-guidelines/naming.html)이 커뮤니티 전체에 적용된다는 점에서 러스트는 다른 언어와 다른 생태계를 갖고 있습니다. 자발적으로 명명 규칙을 잘 지키고 있습니다.&#x20;



