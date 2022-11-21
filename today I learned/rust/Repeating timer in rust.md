---
creation date: 2022-11-20 19:07
modification date: Sunday 20th November 2022 19:07:35
tags: engineering/coding/rust, today_i_leaned
---

# Repeating timer in rust

## Prerequisites
```
cargo add timer
cargo add chrono
```

```rust
use timer;
use chrono;
use std::thread;
use std::sync::{Arc, Mutex};

fn main() {
	let timer = timer::Timer::new();
	// Number of times the callback has been called.
	let count = Arc::new(Mutex::new(0));

	// Start repeating. Each callback increases `count`.
	let guard = {
		let count = count.clone();
		timer.schedule_repeating(chrono::Duration::nanoseconds(500), move || {
			*count.lock().unwrap() += 1;
		})
	};

	// Sleep one second. The callback should be called ~200 times.
	thread::sleep(std::time::Duration::new(1, 0));
	let count_result = *count.lock().unwrap();
	print!("{count_result}");
	assert!(190 <= count_result && count_result <= 210,

	"The timer was called {} times", count_result);

	// Now drop the guard. This should stop the timer.
	drop(guard);
	thread::sleep(std::time::Duration::new(0, 100));

	// Let's check that the count stops increasing.
	let count_start = *count.lock().unwrap();
	thread::sleep(std::time::Duration::new(1, 0));
	let count_stop = *count.lock().unwrap();
	assert_eq!(count_start, count_stop);
}
```