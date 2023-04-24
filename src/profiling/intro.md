# Profiling

In this section, we'll explore how to profile Rspack for identifying bottlenecks.
By examining where Rspack spends its time, we can gain insights into how to improve performance.

<!-- toc -->

## Mac Xcode Instruments

Xcode instruments can be used to produce a CPU profile if you are on a Mac.

To install Xcode Instruments, simply install the Command Line Tools:

```bash
xcode-select --install
```

For normal Rust builds, [`cargo instruments`](https://github.com/cmyr/cargo-instruments) can be used as the glue
for profiling and creating the trace file.

Since Rspack takes quite a while to build, you can use the following procedure without invoking `cargo instruments`.
It has the same effect.

In `crates/node_binding/Cargo.toml`, turn on debug symbols and disable symbol stripping in the `[profile.release]` section

```toml
[profile.release]
debug = true
strip = false
```

Then build the project

```bash
pnpm run build:cli:release
```

The final binary is located at `packages/rspack-cli/bin/rspack` once the project is built.

Under the hood, `cargo instruments` invokes the `xcrun` command,
which means we can run the following in our own project that uses Rspack.

```bash
xcrun xctrace record --template 'Time Profile' --output . --launch -- /path/to/rspack/packages/rspack-cli/bin/rspack build
```

It produces the following output

```
Starting recording with the Time Profiler template. Launching process: rspack.
Ctrl-C to stop the recording
Target app exited, ending recording...
Recording completed. Saving output file...
Output file saved as: Launch_rspack_2023-04-24_11.32.06_9CFE3A63.trace
```

We can open the trace file by

```bash
open Launch_rspack_2023-04-24_11.32.06_9CFE3A63.trace
```
