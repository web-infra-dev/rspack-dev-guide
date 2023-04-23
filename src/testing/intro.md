# Testing

We currently have two sets of test suits, one for Rust and one for Node.js.

### Rust Testing

- `cargo test` will run all the rust side tests, which includes standalone tests for core functionality and plugins.
- `UPDATE=1 cargo test` will automatically update the failed snapshot

### Node Testing

```sh
# In root path
pnpm --filter "./packages/**" run build && pnpm --filter "./packages/**" run test
```

Or only test the package that you made the changes:

```sh
# In the Node.js package path
pnpm run build && pnpm run test
```

### Node Testing Suit Overview

We use jest for nodejs tests, The most important test cases are the case in the `packages/rspack`. most of these cases comes from webpack https://github.com/webpack/webpack/tree/main/test because we want to make sure that Rspack can work as same as webpack.

There are three kinds of integration cases in `@rspack/core`.

#### case.test.ts

Cases are used to test normal build behavior, we use these cases to test against bundler core functionality, like `entry`, `output`, `module` `resolve`, etc. it will first build your test file to test whether the input could be compiled successfully, then it will use the bundled test file to run test cases in the test file to test bundler's all kinds of behavior.

#### configCase.test.ts

Cases are used to test custom build behavior, you could use custom `webpack.config.js` to override default build behavior, you can use these cases to test against behavior related to specific config.

##### statsTestCase.test.ts

Cases are used to test your stats, By Default we will use jest's snapshot to snapshot your stats, and we **highly** recommend to **avoid** snapshot except statsCase. you can use statsCase to test behaviors like code splitting | bundle splitting, which is hard to test by just running code.
