# Debugging

## Debugging with VSCode

1. Install `go install github.com/go-delve/delve/cmd/dlv@latest`
2. Install vscode extension [rust-analyzer](https://marketplace.visualstudio.com/items?itemName=rust-lang.rust-analyzer) and [CodeLLDB](https://marketplace.visualstudio.com/items?itemName=vadimcn.vscode-lldb)
3. build `@rspack/cli` and napi binding by run `pnpm -w build:cli:debug`
4. In Vscode's `Run and Debug` tab, select `debug-rspack` to start debugging the initial launch of `@rspack/cli`, This task is configured in `.vscode/launch.json`, which launch node debugger and rust debugger together. so you can debug both rust and nodejs code.
