# Profiling

In this section, we'll explore how to profile Rspack for identifying bottlenecks.
By examining where Rspack spends its time, we can gain insights into how to improve performance.

<!-- toc -->

## Tracing

[`tracing`](https://crates.io/crates/tracing) is used to instrumenting Rspack.

The supported tracing levels for

* release builds are `INFO`, `WARN` and `ERROR`
* debug builds are `TRACE`, `DEBUG`, `INFO`, `WARN` and `ERROR`

### Chrome

[`tracing-chrome`](https://crates.io/crates/tracing-chrome) is supported for viewing tracing information graphically.

Setting the environment variable `layer` to `chrome` before running Rspack, for example

```bash
layer=chrome TRACE=TRACE pnpm run build
```

produces a trace file (`trace-timestamp.json`) in the current working directory.

The JSON trace file can be viewed in either `chrome://tracing` or [ui.perfetto.dev](https://ui.perfetto.dev).

### Terminal

Granular tracing event values can be viewed inside the terminal via `layer=logger`, for example

```bash
layer=logger TRACE=TRACE pnpm run build
```

will print the options passed to Rspack as well as each individual tracing event.

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
