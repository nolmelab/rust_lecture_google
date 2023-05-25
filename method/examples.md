# 예제

{% code lineNumbers="true" %}
```rust
#[derive(Debug)]
struct Race {
    name: String,
    laps: Vec<i32>,
}

impl Race {
    fn new(name: &str) -> Race {  // No receiver, a static method
        Race { name: String::from(name), laps: Vec::new() }
    }

    fn add_lap(&mut self, lap: i32) {  // Exclusive borrowed read-write access to self
        self.laps.push(lap);
    }

    fn print_laps(&self) {  // Shared and read-only borrowed access to self
        println!("Recorded {} laps for {}:", self.laps.len(), self.name);
        for (idx, lap) in self.laps.iter().enumerate() {
            println!("Lap {idx}: {lap} sec");
        }
    }

    fn finish(self) {  // Exclusive ownership of self
        let total = self.laps.iter().sum::<i32>();
        println!("Race {} is finished, total lap time: {}", self.name, total);
    }
}

fn main() {
    let mut race = Race::new("Monaco Grand Prix");
    race.add_lap(70);
    race.add_lap(68);
    race.print_laps();
    race.add_lap(71);
    race.print_laps();
    race.finish();
    // race.add_lap(42);
}
```
{% endcode %}

코딩해서 직접 확인하고 잘 모르는 부분은 찾아보면서 이해를 해야 합니다.

라인 37의 주석을 풀면 컴파일 에러가 나옵니다.&#x20;

```rust
error[E0382]: borrow of moved value: `race`
   --> src\main.rs:277:9
    |
270 |         let mut race = Race::new("Monaco Grand Prix");
    |             -------- move occurs because `race` has type `Race`, which does not implement the `Copy` trait
...
276 |         race.finish();
    |              -------- `race` moved due to this method call
277 |         race.add_lap(42);
    |         ^^^^^^^^^^^^^^^^ value borrowed here after move
    |
note: this function takes ownership of the receiver `self`, which moves `race`
   --> src\main.rs:261:19
    |
261 |         fn finish(self) {
    |                   ^^^^
```

발표자 노트의 설명입니다.&#x20;

<details>

<summary>발표자 노트</summary>

* 4가지 유형의 메서드 receiver에 대해 설명합니다.
  * receiver 유형에 따라 함수가 할 수 있는 일이 달라지고, 또 메소드를 호출한 뒤 `main`에서 해당 객체를 사용할 수 있는지 여부도 달라진다는 점을 강조하세요.
  * `finish`를 두번 호출하여 오류가 발생하는 것을 보일 수 있습니다.

<!---->

* 비록 메서드 receiver는 다르지만 main 함수에서 비 정적 함수를 부르는 방법은 같습니다. **\[1]** 러스트는 메서드를 호출할 때 자동으로 참조/역참조(따라가기)를 수행합니다. 러스트는 객체와 매서드 시그니처가 서로 매치되도록 객체에 `&`, `*`, `mut`를 자동으로 붙여줍니다.

<!---->

* `print_laps`함수에서 **\[2]** 벡터를 어떤 식으로 사용하고 있는지 언급하는 것도 좋습니다. 벡터는 오후 강의에서 더 자세히 설명할 것입니다.

</details>

<details>

<summary>놀미 노트</summary>

* **\[1]** 자동으로 참조/역참조를 수행한다는 뜻은 `race.add_lap(70)`을 `Race::add_lap(&mut self, 70)`으로 타잎을 잘 찾아서 변환해 준다는 뜻입니다.&#x20;

<!---->

* **\[2]** Vec는 C++의 벡터와 비슷합니다. 연속된 메모리를 갖고 크기를 늘리면서 동일 타잎의 항목을 여러 개 관리합니다. 러스트는 슬라이스를 통해 연속된 메모리를 갖는 타잎들을 처리하는데 이와 연관된 함수들이 많다는 차이가 있습니다. [std::vec::Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html) 문서를 참고하세요.

<!---->

* race.finish()를 호출하면 race의 할당에 해당하는 수신자(receiver)를 finish()가 가지므로 이동됩니다. 그리고, finish()가 종료될 때 race는 Drop 됩니다. 러스트의 메서드들은 수신자가 있고 impl 블럭이 타잎 (구조체나 enum)으로 구분되는 글로벌 함수처럼 동작한다고 생각할 수 있습니다. 클래스처럼 생각하면 self에 할당되면서 이동된다는 개념이 성립하기 어렵기 때문입니다.

</details>
