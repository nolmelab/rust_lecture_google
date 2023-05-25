# 식사하는 철학자들 (Dining Philosophers)

> 5명의 철학자가 원탁에서 식사를 하고 있습니다. 철학자는 원탁에서 자신의 자리에 앉아있습니다. 포크는 각 접시 사이에 있습니다. 제공되는 요리를 먹기 위해서는 두 개의 포크를 모두 사용해야합니다. 철학자는 생각을 하다가 배가 고프면 자신의 좌,우의 포크를 들어 요리를 먹습니다. 철학자는 요리를 먹은 후에는 포크를 다시 자리에 내려놓습니다. 철학자는 자신의 좌,우에 포크가 있을때만 요리를 먹을 수 있습니다. 따라서 두 개의 포크는 오직 자신의 좌,우 철학자가 생각을 할 때만 사용할 수 있습니다.

```rust
use std::sync::{mpsc, Arc, Mutex};
use std::thread;
use std::time::Duration;

struct Fork;

struct Philosopher {
    name: String,
    // left_fork: ...
    // right_fork: ...
    // thoughts: ...
}

impl Philosopher {
    fn think(&self) {
        self.thoughts
            .send(format!("Eureka! {} has a new idea!", &self.name))
            .unwrap();
    }

    fn eat(&self) {
        // Pick up forks...
        println!("{} is eating...", &self.name);
        thread::sleep(Duration::from_millis(10));
    }
}

static PHILOSOPHERS: &[&str] =
    &["Socrates", "Plato", "Aristotle", "Thales", "Pythagoras"];

fn main() {
    // Create forks

    // Create philosophers

    // Make them think and eat

    // Output their thoughts
}
```
