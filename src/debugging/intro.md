# Debugging

## Debugging with VSCode

1. Install `go install github.com/go-delve/delve/cmd/dlv@latest`
2. Install VSCode extension [rust-analyzer](https://marketplace.visualstudio.com/items?itemName=rust-lang.rust-analyzer) and [CodeLLDB](https://marketplace.visualstudio.com/items?itemName=vadimcn.vscode-lldb)
3. build `@rspack/cli` and napi binding by run `pnpm install && pnpm -w build:cli:debug`
4. In VSCode's `Run and Debug` tab, select `debug-rspack` to start debugging the initial launch of `@rspack/cli`. This task can be configured in `.vscode/launch.json`, which launches the Node and Rust debugger together.
