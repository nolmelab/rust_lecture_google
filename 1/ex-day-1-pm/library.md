# 도서관 (Library)

우리는 내일 구조체와 `Vec<T>`에 대해 더 많은 것을 배울 것입니다. 일단 오늘은 API의 일부만 알면 됩니다:

```rust
fn main() {
    let mut vec = vec![10, 20];
    vec.push(30);
    let midpoint = vec.len() / 2;
    println!("middle value: {}", vec[midpoint]);
    for item in &vec {
        println!("item: {item}");
    }
}
```

도서관 프로그램을 만들기 위해 아래 코드를 [https://play.rust-lang.org/](https://play.rust-lang.org/)에 복사해서 구현하시면 됩니다:

```rust
struct Library {
    books: Vec<Book>,
}

struct Book {
    title: String,
    year: u16,
}

impl Book {
    // This is a constructor, used below.
    fn new(title: &str, year: u16) -> Book {
        Book {
            title: String::from(title),
            year,
        }
    }
}

// Implement the methods below. Update the `self` parameter to
// indicate the method's required level of ownership over the object:
//
// - `&self` for shared read-only access,
// - `&mut self` for unique and mutable access,
// - `self` for unique access by value.
impl Library {
    fn new() -> Library {
        todo!("Initialize and return a `Library` value")
    }

    //fn len(self) -> usize {
    //    todo!("Return the length of `self.books`")
    //}

    //fn is_empty(self) -> bool {
    //    todo!("Return `true` if `self.books` is empty")
    //}

    //fn add_book(self, book: Book) {
    //    todo!("Add a new book to `self.books`")
    //}

    //fn print_books(self) {
    //    todo!("Iterate over `self.books` and each book's title and year")
    //}

    //fn oldest_book(self) -> Option<&Book> {
    //    todo!("Return a reference to the oldest book (if any)")
    //}
}

// This shows the desired behavior. Uncomment the code below and
// implement the missing methods. You will need to update the
// method signatures, including the "self" parameter! You may
// also need to update the variable bindings within main.
fn main() {
    let library = Library::new();

    //println!("The library is empty: {}", library.is_empty());
    //
    //library.add_book(Book::new("Lord of the Rings", 1954));
    //library.add_book(Book::new("Alice's Adventures in Wonderland", 1865));
    //
    //println!("The library is no longer empty: {}", library.is_empty());
    //
    //
    //library.print_books();
    //
    //match library.oldest_book() {
    //    Some(book) => println!("The oldest book is {}", book.title),
    //    None => println!("The library is empty!"),
    //}
    //
    //println!("The library has {} books", library.len());
    //library.print_books();
}
```
