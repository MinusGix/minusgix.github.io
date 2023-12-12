{{#include ../include/header012.md}}

The first thing we will do is create a Bevy project. You can use an existing one if you wish.  
See: https://bevyengine.org/learn/book/getting-started/setup/ for the setup.  
  
I also use `bevy_smooth_cameras` but you don't necessarily need that.


```rust
// main.rs
use bevy::{
    prelude::*,
    render::render_resource::{AsBindGroup, ShaderRef},
};
use smooth_bevy_cameras::{
    controllers::unreal::{UnrealCameraBundle, UnrealCameraController, UnrealCameraPlugin},
    LookTransformPlugin,
};

fn main() {
    App::new()
        .add_plugins(DefaultPlugins)
        .add_plugins(LookTransformPlugin)
        .add_plugins(UnrealCameraPlugin::default())
        .add_plugins(MaterialPlugin::<CustomMaterial>::default())
        .add_systems(Startup, setup)
        .add_systems(Update, keybinds)
        .run();
}

fn setup(
    mut commands: Commands,
    mut meshes: ResMut<Assets<Mesh>>,
    mut cmaterials: ResMut<Assets<CustomMaterial>>,
) {
    commands
        .spawn(Camera3dBundle::default())
        .insert(UnrealCameraBundle::new(
            UnrealCameraController::default(),
            Vec3::new(2.0, 7.0, 3.0),
            Vec3::new(0.0, 0.0, 0.0),
            Vec3::Y,
        ));

    commands.spawn(PointLightBundle {
        transform: Transform::from_xyz(4.0, 8.0, 4.0),
        ..Default::default()
    });

    commands.spawn(MaterialMeshBundle {
        mesh: meshes.add(Mesh::from(shape::Box::new(2.0, 2.0, 2.0))),
        material: cmaterials.add(CustomMaterial {}),
        ..Default::default()
    });
}

fn keybinds(mut commands: Commands, keyboard_input: Res<Input<KeyCode>>) {
    if keyboard_input.just_pressed(KeyCode::Escape) {
        std::process::exit(0);
    }
}

#[derive(Asset, TypePath, AsBindGroup, Debug, Clone)]
pub struct CustomMaterial {}
impl Material for CustomMaterial {
    fn fragment_shader() -> ShaderRef {
        "shaders/custom.wgsl".into()
    }

    fn alpha_mode(&self) -> AlphaMode {
        AlphaMode::Blend
    }
}
```

This code spawns a cube. (TODO: just swap to a box since we just use the same length for each side)  
As well, it creates a new material.  
  
The path of the fragment shader should be in your `assets` folder, like so:
```
- my_bevy_project/
  - assets/
    - shaders/
      - custom.wgsl
  - src/
    - main.rs
```

You can put it wherever you want in that folder.  
  
<!-- TODO: use wgsl syntax highlighting -->
```c
#import bevy_pbr::{
    mesh_view_bindings::globals,
    forward_io::VertexOutput,
}

@fragment
fn fragment(in: VertexOutput) -> @location(0) vec4<f32> {
    return vec4<f32>(1.0, 0.0, 0.0, 1.0);
}
```
This is our initial WGSL shader.

The first line acts like a Rust import.  
`bevy_pbr::mesh_view_bindings::globals` has couple common fields, the most important being the `time` which we will use in the future.  
The second import is the `VertexOutput`, which we are taking into the fragment shader function.  

There are three common types of shaders:
- **Vertex Shaders**: These allow positiong vertices (points) and associating information with them.
    - Ex: Leaves that sway in the wind, waves in the ocean, and 
- **Fragment Shaders**: These allow deciding how the fragments (roughly, pixels on a mesh) are colored.
    - Ex: Applying a texture, processing the effect of light, or a lava lamp that shifts between colors.
- **Compute Shaders**: These allow doing general computation on the GPU.
    - Ex: Physics, generating terrain, etc.

