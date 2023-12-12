{{#include ../include/header012.md}}

# Intro Swaying
With our new custom vertex shader, we can do the exceedingly obvious: Make our mesh sway back and forth.  
```rust
@vertex
fn vertex(vertex: Vertex) -> VertexOutput {
    var out: VertexOutput;
    out.position = mesh_position_local_to_clip(get_model_matrix(vertex.instance_index), vec4<f32>(vertex.position, 1.0));
    out.position.x += sin(2.0 * globals.time);
    out.position.y += abs(cos(globals.time));
    return out;
}
``````

// TODO: Add gif

