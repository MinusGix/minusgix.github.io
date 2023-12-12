{{#include ../include/header012.md}}

# Basic Vertex Shaders
Vertex shaders decide how vertices are positioned in clip space, and what information gets passed to the fragment shader. They're run once per vertex.  
  
To declare a fragment shader, we need to alter our `Material` definition:  
```rust
impl Material for CustomMaterial {
    fn vertex_shader() -> ShaderRef {
        "shaders/custom.wgsl".into()
    }

    fn fragment_shader() -> ShaderRef {
        "shaders/custom.wgsl".into()
    }

    fn alpha_mode(&self) -> AlphaMode {
        AlphaMode::Blend
    }
}
```

This tells Bevy that our custom.wgsl also defines a custom vertex shader.  
```c
#import bevy_pbr::{
    mesh_view_bindings::globals,
    mesh_functions::{get_model_matrix, mesh_position_local_to_clip},
    // forward_io::VertexOutput,
}

struct Vertex {
    @builtin(instance_index) instance_index: u32,
    @location(0) position: vec3<f32>,
}

struct VertexOutput {
    @builtin(position) position: vec4<f32>,
}

@vertex
fn vertex(vertex: Vertex) -> VertexOutput {
    var out: VertexOutput;
    // turns vertex position (mesh pos local) into clip position (clip space)
    out.position = mesh_position_local_to_clip(get_model_matrix(vertex.instance_index), vec4<f32>(vertex.position, 1.0));
    return out;
}

@fragment
fn fragment(in: VertexOutput) -> @location(0) vec4<f32> {
    return vec4<f32>(1.0, 0.0, 0.0, 1.0);
}
```

Our vertex shader is quite simple. It takes in a vertex at a (local-space) position and outputs a position in clip-space. Implicitly, the clip-space position is transformed into fragment coordinates.  

