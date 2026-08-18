# bevy-examples

Bevy examples that are too large to keep in the engine repository. Each example is a
separate crate in `examples/`, and all of them share one Cargo workspace.

The examples build against the `main` branch of Bevy, not against a release. The
`Cargo.lock` file is committed, so a new checkout builds against a known good commit of
`main`. Run `cargo update -p bevy` to move to a newer commit.

## Examples

| Example | Description |
| --- | --- |
| [`zero_day`](examples/zero_day) | Beeple's "Zero-Day" corridor, path-traced with Bevy Solari. |

## Running

Always build in release mode. These scenes are large, and a debug build of a path tracer
is too slow to use.

```console
cargo run -p zero_day --release
```

Most of the examples need scene assets that this repository doesn't include. The
`README.md` file of each example tells you how to get them.
