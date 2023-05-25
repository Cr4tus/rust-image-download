# Rust Image Download Experiment

## What does the app do?
The program saves in a temporary file the image found at this url: https://www.rust-lang.org/logos/rust-logo-512x512.png and prints the full path of that file.

## Programming Languages:
- Rust

## Frameworks & Libraries:
- tempfile - https://crates.io/crates/tempfile | https://docs.rs/tempfile/latest/tempfile/
- error-chain - https://crates.io/crates/error-chain | https://docs.rs/error-chain/latest/error_chain/
- tokio - https://tokio.rs | https://docs.rs/tokio/latest/tokio/
- reqwest - https://crates.io/crates/reqwest | https://docs.rs/reqwest/latest/reqwest/

## Implementation:
After declaring at the top of the *main.rs* file the extern crates, we use error-chain's macro to declare the foreign links like:
```rust
error_chain::error_chain! {
    foreign_links {
        Io(std::io::Error);
        HttpRequest(reqwest::Error);
    }
}
```
We then create the temporary directory:
```rust
let temporary_directory = tempfile::Builder::new()
    .prefix("temp-dir")
    .tempdir()?;
```
After that, we make the *GET* request, create the output file and copy the response body inside it.
