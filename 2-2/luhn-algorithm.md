# 룬 알고리즘 (Luhn Algorithm)

[룬(Luhn) 알고리즘](https://ko.wikipedia.org/wiki/%EB%A3%AC\_%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98)은 신용카드 번호 검증에 사용되는 알고리즘 입니다. 이 알고리즘은 신용카드 번호를 `문자열`로 입력받고, 아래의 순서에 따라 신용카드 번호의 유효성을 확인합니다:

* 모든 공백을 무시합니다. 두자리 미만 숫자는 무시합니다.
* 오른쪽에서 왼쪽으로 이동하며 2번째 자리마다 숫자를 2배 증가시킵니다. 예를 들어 `1234`에서 `3`과 `1`에 각각 2를 곱합니다.
* 두배로 만든 숫자가 두자리라면 각 자리 숫자를 더합니다. 예를 들어, `7`은 두배로 만들면 `14`이므로 `5`가 됩니다.
* 모든 자리의 숫자를 더합니다.
* 합계의 끝자리가 `0`인 경우 유효한 신용카드 번호입니다.

아래 코드를 [https://play.rust-lang.org/](https://play.rust-lang.org/)에 복사하고 함수를 구현해 보시기 바랍니다:

```rust
// TODO: remove this when you're done with your implementation.
#![allow(unused_variables, dead_code)]

pub fn luhn(cc_number: &str) -> bool {
    unimplemented!()
}

#[test]
fn test_non_digit_cc_number() {
    assert!(!luhn("foo"));
}

#[test]
fn test_empty_cc_number() {
    assert!(!luhn(""));
    assert!(!luhn(" "));
    assert!(!luhn("  "));
    assert!(!luhn("    "));
}

#[test]
fn test_single_digit_cc_number() {
    assert!(!luhn("0"));
}

#[test]
fn test_two_digit_cc_number() {
    assert!(luhn(" 0 0 "));
}

#[test]
fn test_valid_cc_number() {
    assert!(luhn("4263 9826 4026 9299"));
    assert!(luhn("4539 3195 0343 6467"));
    assert!(luhn("7992 7398 713"));
}

#[test]
fn test_invalid_cc_number() {
    assert!(!luhn("4223 9826 4026 9299"));
    assert!(!luhn("4539 3195 0343 6476"));
    assert!(!luhn("8273 1232 7352 0569"));
}

#[allow(dead_code)]
fn main() {}
```

{% hint style="info" %}
깃북에서 병합이 잘 안 될 때가 있어 보입니다.&#x20;
{% endhint %}
