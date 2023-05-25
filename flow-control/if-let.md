# if let 표현식

if let 표현식을 사용하면 값이 패턴과 일치하는지 여부에 따라 다른 코드를 실행할 수 있습니다:

```rust
fn main() {
    let arg = std::env::args().next();
    if let Some(value) = arg {
        println!("Program name: {value}");
    } else {
        println!("Missing name?");
    }
}
```

<details>

<summary>발표자 노트</summary>

* 한 가지 일치만 처리할 경우 if let이 훨씬 간결합니다. match는 일치하는 모든 경우에 대한 코드가 필요하기 때문입니다.
* 자주 쓰이는  용례중 하나는 Option에 대해 작업할 때 Some 값을 처리하는 것입니다.
* match와 달리 if let은 가드를 지원하지 않습니다.
* let else 문으로 패턴 매칭을 처리할 수 있습니다

```rust
fn main() {
    println!("{:?}", second_word_to_upper("foo bar"));
}
 
fn second_word_to_upper(s: &str) -> Option<String> {
    let mut it = s.split(' ');
    let (Some(_), Some(item)) = (it.next(), it.next()) else {
        return None;
    };
    Some(item.to_uppercase())
}

```



</details>
