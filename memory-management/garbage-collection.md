# 자동 메모리 관리 (Garbage Collection)

수동, 스코프기반 메모리 관리의 대안으로 자동 메모리 관리 방식이 있습니다:

* 개발자는 메모리를 명시적으로 할당/해제 하지 않습니다.
* 가비지 컬렉터(GC)는 사용되지 않는 메모리를 찾아 해제합니다.

## Jave 예제

person객체는 \`sayHello1함수 반환 후에도 해제되지 않습니다. (역주: GC가 나중에 알아서 해제합니다.)

```java
void sayHello(Person person) {
  System.out.println("Hello " + person.getName());
}
```
