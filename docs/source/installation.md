# Installation

With lux:

```shell
lx install rsjson-lua
```

With luarocks:

```shell
luarocks install rsjson-lua
```

With cargo, where `{version}` is one of `55`, `54`, `53`, `52`, or `51`.

```shell
cargo install rsjson-lua --no-default-features --features module,lua{version}
```

Prebuilt binaries:

```shell
lx --extra-servers https://benniekiss.github.io/rocks/ install rsjson-lua
```

Compile from source:

See [building](contributing.md#Building)
