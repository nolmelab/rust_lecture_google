# 무한 채널 (Unbounded Channels)

`mpsc::channel()` 함수는 제한이 없는 비동기 채널을 생성합니다:

```rust
use std::sync::mpsc;
use std::thread;
use std::time::Duration;

fn main() {
    let (tx, rx) = mpsc::channel();

    thread::spawn(move || {
        let thread_id = thread::current().id();
        for i in 1..10 {
            tx.send(format!("Message {i}")).unwrap();
            println!("{thread_id:?}: sent Message {i}");
        }
        println!("{thread_id:?}: done");
    });
    thread::sleep(Duration::from_millis(100));

    for msg in rx.iter() {
        println!("Main: got {}", msg);
    }
}
```

sync\_channel()이 개수에 제한이 있는 채널을 만들기 때문에 따로 제한이 없는 채널이라고 합니다.&#x20;

