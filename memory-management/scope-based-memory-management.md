# 범위 기반 메모리 관리 (Scope-Based Memory Management)

생성자와 소멸자를 사용하여 객체의 생명주기에 따라 메모리 할당/해제가 일어나도록 할 수 있습니다.

포인터를 객체로 감싸도록 하면, 그 객체가 소멸될 때 그 포인터가 가리키는 메모리가 해제되도록 할 수 있습니다. 컴파일러는 객체가 소멸될 때 반드시 소멸자가 호출되는 것을 보장합니다. 심지어는 예외(exception)가 발생(_역주_: 함수의 리턴이나 스코프의 종료 뿐만이 아니라) 하더라도요.

이를 종종 RAII (Resource Acquisition Is Initialization)라고 하며, 이런 객체는 일종의 스마트 포인터 역할을 합니다.

## [C++ 예제](https://google.github.io/comprehensive-rust/ko/memory-management/scope-based.html#c-%EC%98%88%EC%A0%9C) <a href="#c" id="c"></a>

```rust
void say_hello(std::unique_ptr<Person> person) {
  std::cout << "Hello " << person->name << std::endl;
}
```

* `std::unique_ptr`객체는 스택에 할당되며, 힙에 할당된 메모리를 가리킵니다.
* `say_hello`함수가 끝나면 `std::unique_ptr`의 소멸자가 실행됩니다.
* 소멸자는 `Person` 객체가 가리키는 메모리를 해제합니다.

이동 생성자는 함수 호출 시 소유권을 전달할때 사용됩니다:

```rust
std::unique_ptr<Person> person = find_person("Carla");
say_hello(std::move(person));
```
