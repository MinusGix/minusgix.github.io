# FAQ

## My texture is not transparent!
Make sure you put
```rust
fn alpha_mode(&self) -> AlphaMode {
        AlphaMode::Blend
}
```
(or `Add`, or `Multiply`) on the material.