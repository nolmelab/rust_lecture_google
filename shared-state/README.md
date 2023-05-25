# 상태 공유 (Shared State)

러스트는 주로 아래 두 가지 타입을 이용해서 공유 데이터 동기화를 수행합니다:

* [`Arc<T>`](https://doc.rust-lang.org/std/sync/struct.Arc.html), `T`에 대한 아토믹 참조 카운트: 이 참조는 다수의 스레드 사이에서 공유될 수 있고, 참조하던 마지막 스레드가 종료할 경우 `T`를 반환합니다.
* [`Mutex<T>`](https://doc.rust-lang.org/std/sync/struct.Mutex.html): `T`값에 대한 상호 배제 엑세스를 보장합니다.

