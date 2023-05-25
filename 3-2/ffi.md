# FFI 래퍼

러스트는 \_외부 기능 호출(FFI)\_을 지원합니다. 우리는 이를 이용하여 디렉터리에서 파일 이름을 읽어오는 `libc` 함수에 대한 안전한 래퍼를 만들 것입니다.

아래 리눅스 메뉴얼 문서들을 참조하시기 바랍니다:

* [`opendir(3)`](https://man7.org/linux/man-pages/man3/opendir.3.html)
* [`readdir(3)`](https://man7.org/linux/man-pages/man3/readdir.3.html)
* [`closedir(3)`](https://man7.org/linux/man-pages/man3/closedir.3.html)

You will also want to browse the [`std::ffi`](https://doc.rust-lang.org/std/ffi/) module. There you find a number of string types which you need for the exercise:

| Types                                                                                                                                   | Encoding       | Use                            |
| --------------------------------------------------------------------------------------------------------------------------------------- | -------------- | ------------------------------ |
| [`str`](https://doc.rust-lang.org/std/primitive.str.html) and [`String`](https://doc.rust-lang.org/std/string/struct.String.html)       | UTF-8          | Text processing in Rust        |
| [`CStr`](https://doc.rust-lang.org/std/ffi/struct.CStr.html) and [`CString`](https://doc.rust-lang.org/std/ffi/struct.CString.html)     | NUL-terminated | Communicating with C functions |
| [`OsStr`](https://doc.rust-lang.org/std/ffi/struct.OsStr.html) and [`OsString`](https://doc.rust-lang.org/std/ffi/struct.OsString.html) | OS-specific    | Communicating with the OS      |

You will convert between all these types:

* `&str` to `CString`: you need to allocate space for a trailing `\0` character,
* `CString` to `*const i8`: you need a pointer to call C functions,
* `*const i8` to `&CStr`: you need something which can find the trailing `\0` character,
* `&CStr` to `&[u8]`: a slice of bytes is the universal interface for “some unknow data”,
* `&[u8]` to `&OsStr`: `&OsStr` is a step towards `OsString`, use [`OsStrExt`](https://doc.rust-lang.org/std/os/unix/ffi/trait.OsStrExt.html) to create it,
* `&OsStr` to `OsString`: you need to clone the data in `&OsStr` to be able to return it and call `readdir` again.

The [Nomicon](https://doc.rust-lang.org/nomicon/ffi.html) also has a very useful chapter about FFI.

아래 코드를 [https://play.rust-lang.org/](https://play.rust-lang.org/)에 복사하고 빠진 함수와 메서드를 채워봅니다:

```rust
// TODO: remove this when you're done with your implementation.
#![allow(unused_imports, unused_variables, dead_code)]

mod ffi {
    use std::os::raw::{c_char, c_int};
    #[cfg(not(target_os = "macos"))]
    use std::os::raw::{c_long, c_ulong, c_ushort};

    // Opaque type. See https://doc.rust-lang.org/nomicon/ffi.html.
    #[repr(C)]
    pub struct DIR {
        _data: [u8; 0],
        _marker: core::marker::PhantomData<(*mut u8, core::marker::PhantomPinned)>,
    }

    // Layout as per readdir(3) and definitions in /usr/include/x86_64-linux-gnu.
    #[cfg(not(target_os = "macos"))]
    #[repr(C)]
    pub struct dirent {
        pub d_ino: c_long,
        pub d_off: c_ulong,
        pub d_reclen: c_ushort,
        pub d_type: c_char,
        pub d_name: [c_char; 256],
    }

    // Layout as per man entry for dirent
    #[cfg(target_os = "macos")]
    #[repr(C)]
    pub struct dirent {
        pub d_ino: u64,
        pub d_seekoff: u64,
        pub d_reclen: u16,
        pub d_namlen: u16,
        pub d_type: u8,
        pub d_name: [c_char; 1024],
    }

    extern "C" {
        pub fn opendir(s: *const c_char) -> *mut DIR;
        pub fn readdir(s: *mut DIR) -> *const dirent;
        pub fn closedir(s: *mut DIR) -> c_int;
    }
}

use std::ffi::{CStr, CString, OsStr, OsString};
use std::os::unix::ffi::OsStrExt;

#[derive(Debug)]
struct DirectoryIterator {
    path: CString,
    dir: *mut ffi::DIR,
}

impl DirectoryIterator {
    fn new(path: &str) -> Result<DirectoryIterator, String> {
        // Call opendir and return a Ok value if that worked,
        // otherwise return Err with a message.
        unimplemented!()
    }
}

impl Iterator for DirectoryIterator {
    type Item = OsString;
    fn next(&mut self) -> Option<OsString> {
        // Keep calling readdir until we get a NULL pointer back.
        unimplemented!()
    }
}

impl Drop for DirectoryIterator {
    fn drop(&mut self) {
        // Call closedir as needed.
        unimplemented!()
    }
}

fn main() -> Result<(), String> {
    let iter = DirectoryIterator::new(".")?;
    println!("files: {:#?}", iter.collect::<Vec<_>>());
    Ok(())
}
```
