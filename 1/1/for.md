# 배열과 for 문

배열을 아래와 같이 선언 할 수 있음을 배웠습니다:

```rust
let array = [10, 20, 30];
```

배열을 출력하려면 `{:?}`를 씁니다:

```
fn main() {
    let array = [10, 20, 30];
    println!("array: {array:?}");
}
```

러스트에서는 `for` 키워드를 사용해 배열이나 범위를 반복할 수 있습니다:

```
fn main() {
    let array = [10, 20, 30];
    print!("Iterating over array:");
    for n in array {
        print!(" {n}");
    }
    println!();

    print!("Iterating over range:");
    for i in 0..3 {
        print!(" {}", array[i]);
    }
    println!();
}
```

위 코드를 이용해서, 행렬을 예쁘게 출력하는 `pretty_print`함수와, 행렬을 전치(행과 열을 서로 바꾸는)시키는 `transpose`함수를 작성해 보시기 바랍니다:

![](<../../.gitbook/assets/image (5).png>)

두 함수 모두 행렬의 크기는 3 x 3 으로 하드코딩 합니다.

아래 코드를 [https://play.rust-lang.org/](https://play.rust-lang.org/)에 복사해서 구현하시면 됩니다:

```rust
// TODO: 구현이 완료되면 아래 줄은 삭제합니다.
#![allow(unused_variables, dead_code)]

fn transpose(matrix: [[i32; 3]; 3]) -> [[i32; 3]; 3] {
    unimplemented!()
}

fn pretty_print(matrix: &[[i32; 3]; 3]) {
    unimplemented!()
}

fn main() {
    let matrix = [
        [101, 102, 103], // <-- the comment makes rustfmt add a newline
        [201, 202, 203],
        [301, 302, 303],
    ];

    println!("matrix:");
    pretty_print(&matrix);

    let transposed = transpose(matrix);
    println!("transposed:");
    pretty_print(&transposed);
}
```

## [보너스 문제](https://google.github.io/comprehensive-rust/ko/exercises/day-1/for-loops.html#%EB%B3%B4%EB%84%88%EC%8A%A4-%EB%AC%B8%EC%A0%9C) <a href="#undefined" id="undefined"></a>

`&[i32]`슬라이스를 잘 이용하면 행렬 크기를 3 x 3으로 하드코딩 하지 않을 수 있을까요? 예컨데 `&[&[i32]]`는 2차원 슬라이스의 슬라이스 입니다. 가능하다면/하지 않다면 왜 그런가요?

상용 품질의 구현에 대해서는 [`ndarray` 크레이트](https://docs.rs/ndarray/)를 참조하시기 바랍니다.

