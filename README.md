# Rspack Development Guide

> [!NOTE]
> The Rspack dev guide has been merged into the Rspack main website, this repo is no longer maintained. See: <https://rspack.dev/contribute/>.

[![Build Status][ci-badge]][ci-url]

[ci-badge]: https://github.com/web-infra-dev/rspack-dev-guide/actions/workflows/ci.yml/badge.svg?event=push&branch=main
[ci-url]: https://github.com/web-infra-dev/rspack-dev-guide/actions/workflows/ci.yml?query=event%3Apush+branch%3Amain

The development guide is a set of guidelines and instructions that help contributors understand how to work on Rspack. It covers everything from setting up the development environment to coding style and testing guidelines.

[You can read the latest version of the guide here.][book-url]

[book-url]: https://web-infra-dev.github.io/rspack-dev-guide/

The Rspack team believe that creating a development guide for Rspack is a great way to build a good relationship with the open source community. By providing clarity and consistency, lowering barriers to entry, building trust, and encouraging collaboration, we can create a strong and thriving open source project that people will want to contribute to.

## Installation

```bash
cargo install mdbook mdbook-linkcheck mdbook-toc
```

## Preview

```bash
mdbook serve --open
```

# Credits

rspack-dev-guide is deeply inspired by [rustc-dev-guide](https://github.com/rust-lang/rustc-dev-guide), a great example of how to encourage collaboration with the open source community.

# Third Party Licenses

This project partially copies texts from the following projects:

- [rustc-dev-guide(MIT)](https://github.com/rust-lang/rustc-dev-guide)

