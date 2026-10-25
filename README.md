# bun-uv

The `uv` plugin of the Aphrody Bun fork: the `bun-uv` executable that
`bun uv` dispatches to (`src/runtime/cli/plugin_command.rs` in
[aphrody-labs/bun](https://github.com/aphrody-labs/bun)).

Imported from aphrody-labs/bun commit `f31829d8aa36e9f34e662c8a9e5edf6e25705c86` (src/plugins/uv; uv itself is the submodule vendor/uv, aphrody-labs/uv branch bun-0.12.24). That repository keeps the
earlier history.

## Install

Nothing to install: the first `bun uv ...` downloads `bun-uv-<target>` from the
release of the running bun, checks it against that release's `SHA256SUMS.txt`
and caches it in the plugin directory. A `bun-uv` next to the bun executable
takes precedence.

## Build from source

This workspace path-depends on crates of the Bun checkout, so it builds only
mounted in it as `plugins/uv` (an optional submodule, `update = none`):

```sh
git -C <bun checkout> submodule update --init --checkout --recursive plugins/uv
bun bd --target=plugins          # build/<profile>/bun-uv next to bun
# or directly:
cd <bun checkout>/plugins/uv && cargo build --locked --profile plugin -p bun_plugin_uv --bin bun-uv
```

The toolchain is the Bun checkout's `rust-toolchain.toml`. `Cargo.lock` was
derived from the Bun workspace lockfile, so dependency versions match what the
fork built before the move.
