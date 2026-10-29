# btop-mini

`btop-mini` is a terminal-only compact fork of btop for SSH sessions as small as 52×24.

## Controls

- `P`: toggle between the compact dashboard and full-screen process list
- `Up`/`Down`, `Page Up`/`Page Down`: scroll logical CPU cores on the dashboard
- Existing btop process-list keys remain active in process view
- `q`: quit

The dashboard uses btop's native C++ collectors and displays logical cores, load averages, memory, swap, disks, network throughput, and available CPU temperatures.

## Build

```sh
make
./bin/btop-mini
```

To install it as `/usr/local/bin/btop-mini`:

```sh
sudo make install
btop-mini
```

The executable is always named `btop-mini`; it does not replace or conflict with an existing `btop` installation.

GPU support is deliberately disabled in the compact build command because the 52×24 dashboard does not display GPU panels. The source remains cross-platform through btop's existing Linux, macOS, FreeBSD, OpenBSD, and NetBSD collectors.

For a portable static Linux build, add `-DBTOP_STATIC=ON -DBTOP_LTO=OFF`. Prebuilt static Linux executables are provided for x86_64 and ARM64; neither requires an installed C++ runtime.

## Validation

The macOS build was compiled with AppleClang and launched in a 52-column by 24-row pseudo-terminal. The dashboard rendered within bounds, `P` opened process view, a second `P` returned to the dashboard, and `q` restored the terminal. Linux x86_64 and ARM64 static builds compile the upstream Linux collector successfully against musl libc. This Mac cannot execute Linux binaries, so final live 52×24 runtime verification on Linux remains recommended.
