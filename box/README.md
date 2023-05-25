# Box

{% hint style="warning" %}
&#x20;회사에서 편집한 표준 라이브러리 내용이 사라졌습니다. 깃북에서 작업이 처음이라 익숙하지 않은 면이 있나 봅니다. 어려운 상황에 부딪히지만 이를 넘어서야 앞으로 나아갈 수 있습니다. 모두 화이팅!
{% endhint %}

[`Box`](https://doc.rust-lang.org/std/boxed/struct.Box.html)는 힙 데이터에 대한 소유 포인터입니다:

```rust
fn main() {
    let five = Box::new(5);
    println!("five: {}", *five);
}
```

`Box`에 들어있는 `five`를 일반 변수처럼 다룰 수 있고, 범위를 벗어나 수명이 다하면 자동으로 해제(`Drop`을 통해) 합니다.&#x20;

`Box<T>`는 `Deref<Target = T>`를 구현합니다. 이는 `Box<T>`에서 `T` 메서드를 직접 호출할 수 있다는 의미입니다.&#x20;

<figure><img src="../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption><p>Box의 메모리 참조</p></figcaption></figure>

<details>

<summary>발표자 노트</summary>

* `Box`는 C++의 `std::unique_ptr`과 비슷합니다. 차이라면 `Box`는 널이 아님을 보장한다는 점입니다.
* `Deref` 덕분에 위 예제의 `println!`문에 사용된 `*`를 빼도 문제가 없습니다.
* `Box`는 아래의 경우에 유용합니다:
  * 타입 크기를 컴파일 시점에 알 수 없는 경우.
  * 아주 큰 데이터의 소유권을 전달하고 싶은 경우. 스택에 있는 큰 데이터를 복사하는 대신 `Box`를 이용하여 데이터는 힙에 저장하고 포인터만 이동하면 됩니다.

처음에 Box를 만나면 포인터 사용에 익숙한 경우&#x20;

</details>



