# 메서드 수신자(Receiver)

메서드 수진자는 self, mut self, \&self, \&mut self가 있습니다. 함수에 const를 지정하지 않고 수신자를 self나 \&self로 하면 변경이 불가능하므로 훨씬 더 잘 변경 불가능하도록 할 수 있습니다. 소유권만큼 실질적으로 안정성에 큰 도움이 되는 기능입니다.&#x20;

* `&self`: 호출자로부터 공유가능한 불변 참조 방식으로 객체를 빌려옴을 나타냅니다. 객체는 메소드 호출 뒤에도 사용될 수 있습니다.
* `&mut self`: 호출자로부터 유일한 가변 참조 방식으로 객체를 빌려옴을 나타냅니다. 객체는 메소드 호출 뒤에도 사용될 수 있습니다.
* `self`: 호출자로부터 객체의 소유권을 가져오고 객체는 호출자로부터 메소드로 이동됩니다. 메소드가 객체를 소유하게 되며 따라서 명시적으로 소유권을 다른 곳으로 전달하지 않는다면 메서드 종료와 함께 객체는 drop(해제)됩니다.
* `mut self`: 위와 동일하지만 메서드가 객체의 소유권을 가지면서 동시에 객체를 수정할 수도 있습니다. 소유권을 가지는 것이 수정할 수 있음을 의미하는 것은 아닙니다.
* 리시버 없음: 구조체의 정적 메서드가 됩니다. 주로 생성자를 만들때 사용하게 되며, 생성자는 흔히 `new`라고 이름붙입니다.

<details>

<summary>발표자 노트</summary>

“공유가능한 불변“과 “유일한 가변” 부분은 강조할 만합니다. 이러한 제약은 러스트의 빌림 검사기(borrow checker) 규칙으로 늘 붙어 다닙니다. `self`도 예외는 아닙니다. 여러 위치에서 구조체를 참조하는 동시에  객체를 수정하는(`&mut self`를 리시버로 하는) 메서드를 호출하는 것은 불가능합니다.

</details>

<details>

<summary>놀미 노트</summary>

메서드의 수신자도 가변/불변, 빌림의 규칙을 일관되게 적용 받습니다.&#x20;

구조체에 대한 참조가 있을 경우 (가변이건 불변이건) \&mut self를 수신자로 하는 메서드를 호출하게 되면 가변 참조를 얻어야 하는데 이는 빌림 규칙에 어긋납니다.

</details>
