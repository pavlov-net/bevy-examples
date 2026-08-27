# Zero-Day

Beeple's "Zero-Day" corridor from NVIDIA ORCA, path-traced with Bevy Solari. All of the
light comes from about 10,000 emissive triangles, and Solari turns these triangles into
area lights. The example plays the animation of the film and follows the film camera.

## Getting the scene

Download the converted glTF binaries from the
[`zero-day-assets-v1` release](https://github.com/pavlov-net/bevy-examples/releases/tag/zero-day-assets-v1)
into the `assets/` folder of this example. The example loads `measure_one` by default;
the other two measures are optional.

```console
curl -L -o examples/zero_day/assets/zero_day_measure_one.glb \
  https://github.com/pavlov-net/bevy-examples/releases/download/zero-day-assets-v1/zero_day_measure_one.glb

curl -L -o examples/zero_day/assets/zero_day_measure_seven.glb \
  https://github.com/pavlov-net/bevy-examples/releases/download/zero-day-assets-v1/zero_day_measure_seven.glb

curl -L -o examples/zero_day/assets/zero_day_measure_seven_colored_lights.glb \
  https://github.com/pavlov-net/bevy-examples/releases/download/zero-day-assets-v1/zero_day_measure_seven_colored_lights.glb
```

### Converting from source

Alternatively, download the FBX scene from
[NVIDIA ORCA](https://developer.nvidia.com/orca/beeple-zero-day) and convert it yourself.
Bevy can't read FBX files, so the `convert.py` script converts each measure into a glTF
binary with Blender 4 or Blender 5.

```console
blender --background --python-exit-code 1 --python convert.py -- \
  "MEASURE_ONE/MEASURE_ONE.fbx" \
  "examples/zero_day/assets/zero_day_measure_one.glb"

blender --background --python-exit-code 1 --python convert.py -- \
  "MEASURE_SEVEN/MEASURE_SEVEN.fbx" \
  "examples/zero_day/assets/zero_day_measure_seven.glb"

blender --background --python-exit-code 1 --python convert.py -- \
  "MEASURE_SEVEN/MEASURE_SEVEN_COLORED_LIGHTS.fbx" \
  "examples/zero_day/assets/zero_day_measure_seven_colored_lights.glb"
```

## Running

```console
cargo run -p zero_day --release
```

To load a different measure, add `--scene measure_seven` or `--scene
measure_seven_colored_lights`. Run the example with `--help` to see all of the options.

Press `C` to change between the film camera and free flight. Press `N` to turn DLSS Ray
Reconstruction on and off. Press `B` to run a short benchmark. The benchmark prints its
result to the console.

## DLSS

The `dlss` feature denoises the output of Solari with DLSS Ray Reconstruction. It needs an
NVIDIA RTX GPU and the DLSS SDK, so it's off by default.

```console
cargo run -p zero_day --release --features dlss
```

## Scene license

"Zero-Day" is by Mike Winkelmann (Beeple), distributed through
[NVIDIA ORCA](https://developer.nvidia.com/orca/beeple-zero-day) under
[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). The `.glb` files in the
release are modified from the original: converted from FBX to glTF, materials rebuilt,
hidden meshes removed, and animations baked. The code of this example is MIT/Apache-2.0
like the rest of this repository.
