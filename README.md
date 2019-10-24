# docunit

CLI for verifying ascidoctor documentation by executing unit tests that can verfy their correctness.

![](./docs/logo.png)

## Getting started

1. Apply comment into your ascidocs files

```
// doc::test Test.js
```

2. Build your test file in  `doctest/Test.js`

```js
const http = require('http');
const test = require('ava');
const got = require('got');
const listen = require('test-listen');
const app = require('../app');

test.before(async t => {
	t.context.server = http.createServer(app);
	t.context.baseURL = await listen(t.context.server);
});

test.after.always(t => {
	t.context.server.close();
});

test.serial('get /user', async t => {
	const res = await got('/user', { baseURL: t.context.baseURL, json: true });
	t.is(res.body.email, 'test@user.com');
});
```

## Features

- Repeatable testing of your documentation
- Reporting documentation failures

## Local Development

Below is a list of commands you will probably find useful.

### `npm start` or `yarn start`

Runs the project in development/watch mode. Your project will be rebuilt upon changes. TSDX has a special logger for you convenience. Error messages are pretty printed and formatted for compatibility VS Code's Problems tab.

<img src="https://user-images.githubusercontent.com/4060187/52168303-574d3a00-26f6-11e9-9f3b-71dbec9ebfcb.gif" width="600" />

Your library will be rebuilt if you make edits.

### `npm run build` or `yarn build`

Bundles the package to the `dist` folder.
The package is optimized and bundled with Rollup into multiple formats (CommonJS, UMD, and ES Module).

<img src="https://user-images.githubusercontent.com/4060187/52168322-a98e5b00-26f6-11e9-8cf6-222d716b75ef.gif" width="600" />

### `npm test` or `yarn test`

Runs the test watcher (Jest) in an interactive mode.
By default, runs tests related to files changed since the last commit.
