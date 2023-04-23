# How to build and run the compiler

Please see [prerequisites](prerequisites.md) for setting up Rust and Node.js.

## zx —— The build tool Rspack using

### Running setup script

Make sure you are under the workspace root

```bash
node ./scripts/meta/setup.js
```

### Install Node.js dependencies

Install Node.js dependencies via [pnpm](https://pnpm.io/).

```bash
# enable pnpm with corepack, only available on node >= `v14.19.0`
corepack enable

# or install pnpm directly
npm install -g pnpm@7

# Install dependencies
pnpm run init
```

### Setup protoc for sass-embedded

- Install [protoc](https://grpc.io/docs/protoc-installation/) for building `sass-embedded`.

## Building Rspack

- Run `cargo build` to compile Rust code.
- Run `pnpm run build:cli:debug` to compile both Node.js and Rust code.
