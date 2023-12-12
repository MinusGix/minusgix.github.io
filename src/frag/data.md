{{#include ../include/header012.md}}

# Data

Related official example: [shader_material.rs](https://github.com/bevyengine/bevy/blob/v0.12.1/examples/shader/shader_material.rs) + [custom_material.wgsl](https://github.com/bevyengine/bevy/blob/v0.12.1/assets/shaders/custom_material.wgsl)

So we have the ability to make some time dependent effects, or carefully draw things based on their position, but how do we pass data in?  
Or, rather, what is data useful for?  
The most obvious is textures! But there's many different ways to use data. You could use it to pass in information about enemy health which alters their skin, the time (just like that global!), perhaps a roguelike turn counter..

```rust
#[derive(Asset, TypePath, AsBindGroup, Debug, Clone)]
pub struct CustomMaterial {
    #[uniform(0)]
    pub color: Color,
}
```
'uniform' is just meaning that it is the same across all the invocations of the shader. So all the little GPU threads drawing your fragments will have the same color.

Make sure to construct the `CustomMaterial` with some color of your cboice.  
  
```c
@group(1) @binding(0) var<uniform> color: vec4<f32>;

@fragment
fn fragment(in: VertexOutput) -> @location(0) vec4<f32> {
    return color;
}
```
(Note: on `main`, this is `@group(2)` instead!)  

This has the obvious outcome. Choose the color from your Rust code, and then return it in the fragment shader.  
  
Note: The number you choose matters! It is what goes in `@binding`.