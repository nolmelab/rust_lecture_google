# 수동 메모리 관리 (Manual Memory Management)

사용자가 직접 메모리를 할당, 해제 합니다.

조심하지 않으면, 크래시(crash), 버그, 보안취약성 및 메모리 누출이 발생할 수 있습니다.

## [C 언어 예제](https://google.github.io/comprehensive-rust/ko/memory-management/manual.html#c-%EC%96%B8%EC%96%B4-%EC%98%88%EC%A0%9C) <a href="#c" id="c"></a>

`malloc`으로 할당하는 포인터마다 `free`를 호출해야 합니다:

```c
void foo(size_t n) {
    int* int_array = (int*)malloc(n * sizeof(int));
    //
    // ... lots of code
    //
    free(int_array);
}
```

만약 `malloc` 과 `free` 사이에서 함수가 일찍 반환되면 메모리 누출이 일어납니다: 포인터를 잃어버리게 되어 메모리를 반환할 수 없게 됩니다.
