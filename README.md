# bevy-examples

Standalone [Bevy](https://bevy.org) examples that are too large, too asset-heavy, or too
niche to live in the engine repo. Each example is its own crate under `examples/`, sharing
one Cargo workspace.

These track Bevy's `main` branch, not a published release. `Cargo.lock` is committed, so a
fresh checkout builds against a known-good commit; `cargo update -p bevy` moves to a newer
`main`.

## Examples

None yet. Each one lands as its own crate under `examples/`, picked up by the
`examples/*` workspace glob.

## Running

```console
cargo run -p <example> --release
```

Release mode matters: these are heavy scenes, and a debug build of a path tracer is
unusably slow. The workspace already optimizes dependencies in `dev` builds for the same
reason.

Most examples need scene assets that are licensed separately from this repo and are not
checked in. See each example's `README.md` for where to download them and how to convert
them.

## Linux dependencies

Bevy's default features include the Wayland and X11 backends, ALSA audio, and gamepad
support, so a Linux build needs their development packages:

```console
sudo apt-get install libasound2-dev libudev-dev libwayland-dev libxkbcommon-dev
```

See [Bevy's Linux setup notes](https://github.com/bevyengine/bevy/blob/main/docs/linux_dependencies.md)
for other distributions.

## Faster builds

Copy `.cargo/config_fast_builds.toml` to `.cargo/config.toml` and follow the comments in
it to enable a faster linker. This is the same file Bevy ships.

## License

The example code is dual-licensed under [MIT](LICENSE-MIT) or
[Apache-2.0](LICENSE-APACHE), matching Bevy. Scene assets are **not** covered by these
licenses — each carries its own terms from its original source.
