# FromIterator

어떤 컬렉션이 [`FromIterator`](https://doc.rust-lang.org/std/iter/trait.FromIterator.html)를 구현하고 있다면 [`Iterator`](https://doc.rust-lang.org/std/iter/trait.Iterator.html)로부터 그 컬렉션을 만들 수 있습니다

```rust
fn main() {
    let primes = vec![2, 3, 5, 7];
    let prime_squares = primes
        .into_iter()
        .map(|prime| prime * prime)
        .collect::<Vec<_>>();
}
```

위 코드를 자세히 이해해 볼 필요가 있습니다.

```rust
impl<T, A: Allocator> IntoIterator for Vec<T, A> {
    type Item = T;
    type IntoIter = IntoIter<T, A>;

    fn into_iter(self) -> IntoIter<T, A> {
      // ...
    }
    
```

여기의IntoIter는 vec 모듈 안에 구현되어 있고, Iterator를 구현합니다.&#x20;

```rust
impl<T, A: Allocator> Iterator for IntoIter<T, A> 
// ...
```

`map`의 이 `Iterator` 트레이트에 대해 동작하고, `Map<Self,  F>`를 돌려줍니다.

```rust
fn map<B, F>(self, f: F) -> Map<Self, F>
where
    Self: Sized,
    F: FnMut(Self::Item) -> B,
{
  // ...
}
```

`Map`도 `Iterator`를 구현하고 있고 `next()`에서 변환을 합니다.&#x20;

```rust
fn next(&mut self) -> Option<B> {
    self.iter.next().map(&mut self.f)
}
// ... 
```

`next()`는 `Option<T>`를 돌려주고, 그 다음 `map`은 `Option`의 메서드입니다.

```rust
pub const fn map<U, F>(self, f: F) -> Option<U>
where
    F: ~const FnOnce(T) -> U,
    F: ~const Destruct,
{
    match self {
        Some(x) => Some(f(x)),
        None => None,
    }
}
```

마지막 collect() 메서드는 Iterator에 구현되어 있고, 마지막 Iterator인 Map에 대해 동작합니다.&#x20;

```rust
fn collect<B: FromIterator<Self::Item>>(self) -> B
where
    Self: Sized,
{
    FromIterator::from_iter(self)
}
```

`collect::<Vec<_>>`는 Vec에 구현된 FromIterator를 사용하도록 합니다.&#x20;

```rust
impl<T> FromIterator<T> for Vec<T> {
    fn from_iter<I: IntoIterator<Item = T>>(iter: I) -> Vec<T> {
        <Self as SpecFromIter<T, I::IntoIter>>::from_iter(iter.into_iter())
    }
}

impl<T, I> SpecFromIter<T, I> for Vec<T>
where
    I: Iterator<Item = T>,
{
    default fn from_iter(iterator: I) -> Self {
        SpecFromIterNested::from_iter(iterator)
    }
}

impl<T, I> SpecFromIterNested<T, I> for Vec<T>
where
    I: Iterator<Item = T>,
{
    default fn from_iter(mut iterator: I) -> Self {
        // Unroll the first iteration, as the vector is going to be
        // expanded on this iteration in every case when the iterable is not
        // empty, but the loop in extend_desugared() is not going to see the
        // vector being full in the few subsequent loop iterations.
        // So we get better branch prediction.
        let mut vector = match iterator.next() {
            None => return Vec::new(),
            Some(element) => {
                let (lower, _) = iterator.size_hint();
                let initial_capacity =
                    cmp::max(RawVec::<T>::MIN_NON_ZERO_CAP, lower.saturating_add(1));
                let mut vector = Vec::with_capacity(initial_capacity);
                unsafe {
                    // SAFETY: We requested capacity at least 1
                    ptr::write(vector.as_mut_ptr(), element);
                    vector.set_len(1);
                }
                vector
            }
        };
        // must delegate to spec_extend() since extend() itself delegates
        // to spec_from for empty Vecs
        <Vec<T> as SpecExtend<T, I>>::spec_extend(&mut vector, iterator);
        vector
    }
```

실제 벡터 내용을 `Iterator` (여기서는 Map)에서 채우는 건 `spec_extend()`를 거쳐 아래 메서드 `extend_desugared()`에서 진행한다.

```rust
fn extend_desugared<I: Iterator<Item = T>>(&mut self, mut iterator: I) {
    // This is the case for a general iterator.
    //
    // This function should be the moral equivalent of:
    //
    //      for item in iterator {
    //          self.push(item);
    //      }
    while let Some(element) = iterator.next() {
        let len = self.len();
        if len == self.capacity() {
            let (lower, _) = iterator.size_hint();
            self.reserve(lower.saturating_add(1));
        }
        unsafe {
            ptr::write(self.as_mut_ptr().add(len), element);
            // Since next() executes user code which can panic we have to bump the length
            // after each step.
            // NB can't overflow since we would have had to alloc the address space
            self.set_len(len + 1);
        }
    }
}
```

구현 내용이 `Vec`에 대해 길지만 `FromIterator`는 개념상 `Iterator`로 부터 해당 컬렉션을 만들 수 있다는 뜻입니다.

컬렉션 또는 컨테이너를 각 언어에 대해 만드는 작업은 매우 중요하고 노력을 많이 필요로 합니다. Vec 코드도 내부적으로 러스트의 다양한 기능을 활용하여 러스트에 맞게 구현한 내용으로 한번 읽고 구현의 세부 내용을 이해하기는 어렵습니다. 하지만, 어느 정도 시간이 지나면 C++ 코드를 읽는 것보다는 훨씬 수월해지고 즐거움도 함께 합니다.



<details>

<summary>발표자 노트</summary>

`Iterator`에는 다음 함수가 정의되어 있습니다: `fn collect<B>(self) -> B where B: FromIterator<Self::Item>, Self: Sized`

`Iterator<Item = Result<V, E>>`을 `Result<Vec<V>, E>`로 변환할 수 있는 멋진 기능들도 구현되어 있습니다.

</details>
