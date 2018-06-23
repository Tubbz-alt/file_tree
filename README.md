file_tree
=========

[![](http://meritbadge.herokuapp.com/file_tree)](https://crates.io/crates/file_tree)

Creates and manages a directory structure suitable for storing large numbers 
of files (up to 1 trillion).

Usage
-----

Add this to your `Cargo.toml`:

```toml
[dependencies]
file_tree = "^0.1.0"
```

and this to your crate root:

```rust
extern crate file_tree;
```

Examples
--------

Use `FileTree::new(false)` to create a temporary structure that will be deleted
when the created struct is dropped.

Calls to `get_new_file()` will generate a new `PathBuf`, but will not actually
create the file. 

```rust
extern crate file_tree;

use file_tree::FileTree;

fn main() {
    let mut file_tree = FileTree::new(false).unwrap();

    let writeable_path = file_tree.get_new_file().unwrap();
    assert_eq!(
        writeable_path,
        file_tree.get_root().join("000/000/000/000000000000")
    );

    let writeable_path_2 = file_tree.get_new_file().unwrap();
    assert_eq!(
        writeable_path_2,
        file_tree.get_root().join("000/000/000/000000000001")
    );
}

```