# 다각형 구조체

우리는 몇개의 꼭지점을 가진 다각형을 표현하는 `Polygon` 구조체를 만들 것입니다. 아래 코드를 [https://play.rust-lang.org/](https://play.rust-lang.org/)에 복사해서 테스트가 통과하도록 빠진 메서드를 구현하시면 됩니다:

```rust
// TODO: remove this when you're done with your implementation.
#![allow(unused_variables, dead_code)]

pub struct Point {
    // add fields
}

impl Point {
    // add methods
}

pub struct Polygon {
    // add fields
}

impl Polygon {
    // add methods
}

pub struct Circle {
    // add fields
}

impl Circle {
    // add methods
}

pub enum Shape {
    Polygon(Polygon),
    Circle(Circle),
}

#[cfg(test)]
mod tests {
    use super::*;

    fn round_two_digits(x: f64) -> f64 {
        (x * 100.0).round() / 100.0
    }

    #[test]
    fn test_point_magnitude() {
        let p1 = Point::new(12, 13);
        assert_eq!(round_two_digits(p1.magnitude()), 17.69);
    }

    #[test]
    fn test_point_dist() {
        let p1 = Point::new(10, 10);
        let p2 = Point::new(14, 13);
        assert_eq!(round_two_digits(p1.dist(p2)), 5.00);
    }

    #[test]
    fn test_point_add() {
        let p1 = Point::new(16, 16);
        let p2 = p1 + Point::new(-4, 3);
        assert_eq!(p2, Point::new(12, 19));
    }

    #[test]
    fn test_polygon_left_most_point() {
        let p1 = Point::new(12, 13);
        let p2 = Point::new(16, 16);

        let mut poly = Polygon::new();
        poly.add_point(p1);
        poly.add_point(p2);
        assert_eq!(poly.left_most_point(), Some(p1));
    }

    #[test]
    fn test_polygon_iter() {
        let p1 = Point::new(12, 13);
        let p2 = Point::new(16, 16);

        let mut poly = Polygon::new();
        poly.add_point(p1);
        poly.add_point(p2);

        let points = poly.iter().cloned().collect::<Vec<_>>();
        assert_eq!(points, vec![Point::new(12, 13), Point::new(16, 16)]);
    }

    #[test]
    fn test_shape_perimeters() {
        let mut poly = Polygon::new();
        poly.add_point(Point::new(12, 13));
        poly.add_point(Point::new(17, 11));
        poly.add_point(Point::new(16, 16));
        let shapes = vec![
            Shape::from(poly),
            Shape::from(Circle::new(Point::new(10, 20), 5)),
        ];
        let perimeters = shapes
            .iter()
            .map(Shape::perimeter)
            .map(round_two_digits)
            .collect::<Vec<_>>();
        assert_eq!(perimeters, vec![15.48, 31.42]);
    }
}

#[allow(dead_code)]
fn main() {}
```

테스트를 갖는 매우 좋은 구조를 갖춘 연습문제입니다.&#x20;

<details>

<summary>발표자 노트</summary>

누락된 메서드 시그니처를 올바르게 정의하는 것이 문제의 핵심 부분입니다. 테스트는 수정하면 안됩니다.

연습문제의 다른 흥미로운 부분:

* 테스트 코드를 보면 어떤 메서드들은 인자를 borrow하는 대신 `Copy` 트레잇을 사용하기도 합니다. 구조체가 `Copy` 트레잇을 상속(derive)하도록 하면 됩니다.
* **\[1]** “+“를 사용하여 두 객체를 서로 더하려면 `Add` 트레잇을 구현해야 합니다. 이는 3일차에 다룰 내용입니다.

</details>

<details>

<summary>놀미 노트</summary>

**\[1]** Add 트레이트와 같은 컴파일러가 제공하는 트레이트들로 연산자를 임의의 타잎 (구조체와 열거형)에 대해 구현할 수 있습니다.&#x20;

이들 연산자 트레이트들은 std::ops 모듈을 참고하세요

</details>
