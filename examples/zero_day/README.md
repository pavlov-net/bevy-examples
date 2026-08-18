# Zero-Day

Beeple's "Zero-Day" corridor from NVIDIA ORCA, path-traced with Bevy Solari. All of the
light comes from about 10,000 emissive triangles, and Solari turns these triangles into
area lights. The example plays the animation of the film and follows the film camera.

## Getting the scene

Download the scene from [NVIDIA ORCA](https://developer.nvidia.com/orca/beeple-zero-day).

Bevy can't read FBX files, so you must convert the measures that you want into glTF
binaries. The `convert.py` script does this with Blender 4 or Blender 5. Put the result in
the `assets/` folder of this example.

```console
blender --background --python-exit-code 1 --python convert.py -- \
  "MEASURE_ONE/MEASURE_ONE.fbx" \
  "examples/zero_day/assets/zero_day_measure_one.glb"
```

The example loads `measure_one` by default. The other two measures are optional, and you
convert them with the same command.

```console
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
