# Runtimes

런타임은 비동기적으로 연산을 수행하는 것을 지원하며(리액터), Future 실행(Executor)을 담당합니다. Rust에는 "내장" 런타임이 없지만 몇 가지 옵션을 사용할 수 있습니다:

* [Tokio](https://tokio.rs/) - 성능이 뛰어나며, HTTP용 [Hyper](https://hyper.rs/) 또는 gRPC용 [토닉](https://github.com/hyperium/tonic)과 같이 잘 개발된 기능 생태계를 갖추고 있습니다.&#x20;
* [async-std](https://async.rs/) - "비동기를 위한 std"를 목표로 하며, async::task에 기본 런타임이 포함되어 있습니다.&#x20;
* [smol](https://docs.rs/smol/latest/smol/) - 간단하고 가벼운 런타임

몇몇 대형 애플리케이션에는 자체 런타임이 있습니다. 예를 들어 [Fuchsia](https://fuchsia.dev/)에는 이미 런타임이 있습니다.

<details>

<summary>발표자 노트</summary>

* 나열된 런타임 중 Rust 플레이그라운드에서는 Tokio만 지원된다는 점에 유의하세요. 또한 플레이그라운드는 I/O를 허용하지 않으므로 대부분의 흥미로운 비동기 동작은 플레이그라운드에서 실행할 수 없습니다.
* 퓨처는 실행자가 폴링하지 않는 한 아무것도 하지 않는다는 점에서 "비활성"입니다(심지어 I/O 작업을 시작하지도 않음). 이는 예를 들어 한 번도 사용되지 않더라도 완료될 때까지 실행되는 JS 프로미스와는 다릅니다



</details>
