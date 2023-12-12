{{#include ./include/header012.md}}

# Extended Material
Relevant official example: [extended_material.rs](https://github.com/bevyengine/bevy/blob/v0.12.1/examples/shader/extended_material.rs), [extended_material.wgsl](https://github.com/bevyengine/bevy/blob/v0.12.1/assets/shaders/extended_material.wgsl)

Okay, we do NOT want to implement all of lighting, normal maps, and more by ourselves!  
Surely there's a better way.  
  
The better way specifically is to use [ExtendedMaterial](https://docs.rs/bevy/latest/bevy/pbr/struct.ExtendedMaterial.html). At least it is right now, this was added recently. Before you had to manually copy the sizable PBR shader and strip out the parts you didn't want.  

[pbr.wgsl](https://github.com/bevyengine/bevy/blob/v0.12.1/crates/bevy_pbr/src/render/pbr.wgsl) but that isn't so bad... mostly due to the developers reasonably spreading it out across multiple files. Skim over some of the files in the same directory, it can be a good way to familiarize and confuse yourself about shaders.  
  
Anyway, we don't need that! Mostly.
... Just scroll up and open the official example. There's no reason to copy it wholesale into here, it does a good job at showing off the idea.  
  
TODO: more explanation of individual parts of the example.