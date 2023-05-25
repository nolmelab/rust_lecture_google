# (함수) 오버로딩

러스트에서 한 이름의 함수는 하나입니다.&#x20;

* 가변 개수의 파라미터는 매크로로 처리합니다.
* 파리미터가 제네릭 타잎을 가질 수 있습니다.

```rust
fn pick_one<T>(a: T, b: T) -> T {
    if std::process::id() % 2 == 0 { a } else { b }
}

fn main() {
    println!("coin toss: {}", pick_one("heads", "tails"));
    println!("cash prize: {}", pick_one(500, 1000));
}
```
