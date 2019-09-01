# Create-React-Extension [![PRs Welcome](https://img.shields.io/badge/PRs-welcome-green.svg)](https://github.com/VasilyShelkov/create-react-extension/pulls)

Create React browser extensions with no build configuration.

This is a fork of [create-react-app](https://github.com/facebook/create-react-app) to make creating Browser Extensions in React more accessible and following
[Create-React-App's(CRA) philosophy](https://github.com/facebook/create-react-app#philosophy), especially **convention over configuration**.

## Features

- [x] [Same CRA Developer Experience](https://github.com/facebook/create-react-app#whats-included) for your browser extension projects (~~service worker functionality~~)
- [x] [Webpack dev server](https://github.com/webpack/webpack-dev-server) hot reloads extension on changes (NOTE: contentScript hot reloading not supported)
- [x] [Supports any combination of background, content and popup chrome extensions](#only-1-new-convention)
- [ ] Add e2e test suite similar to the [original CRA](https://github.com/facebook/create-react-app/tree/master/test) and run with automated pipeline.
- [ ] Add [automated fork watcher](https://github.com/wei/pull) to stay updated with the original CRA
- [ ] Add some kind of dependency watcher (e.g. [greenkeeper](https://greenkeeper.io/)) to stay up to date with the dependencies that are not managed by CRA

see [Create a browser extension](#creating-a-browser-extension) for a more in depth start guide
see [CRA user guide](https://facebook.github.io/create-react-app/) for more information on different configurations and functionality available.

If something doesn’t work, please [file an issue](https://github.com/VasilyShelkov/create-react-extension/issues/new).

## Quick Overview

```sh
npx create-react-app my-browser-extension --scripts-version react-browser-extension-scripts
cd my-browser-extension
npm start
```

_([npx](https://medium.com/@maybekatz/introducing-npx-an-npm-package-runner-55f7d4bd282b) comes with npm 5.2+ and higher, see [instructions for older npm versions](https://gist.github.com/gaearon/4064d3c23a77c74a3614c498a8bb1c5f))_

Then open Chrome, and unpack the newly created `/dev` folder to see your extension added locally to your browser.<br>
When you’re ready to ship your extension, create an optimized build with `npm run build`.

<p align='center'>
<img src='https://cdn.rawgit.com/facebook/create-react-app/27b42ac/screencast.svg' width='600' alt='npm start'>
</p>

## What's do I need to know to start building my extension ?

It's follows mostly the [same conventions as CRA](https://github.com/facebook/create-react-app#get-started-immediately).

### Only 1 new convention

There are [different types of chrome extensions](https://developer.chrome.com/extensions/getstarted) which can be any combination of:

- [Popup UI](https://developer.chrome.com/extensions/user_interface#popup) which renders your `index.js` when you click on your extension in the browser extension icon.
- [Background script](https://developer.chrome.com/extensions/background_pages) which will run in the background from `/background/index.js` and can be use for things like [state-management](https://github.com/tshaddix/webext-redux).
- [Content script](https://developer.chrome.com/extensions/content_scripts) from `/contentScript/index.js` which will run on configured web pages
- [Options UI](https://developer.chrome.com/extensions/options) :cross: Does not support yet

These are all controlled by the all important [`/public/manifest.json`](https://github.com/VasilyShelkov/create-react-extension/blob/master/packages/react-scripts/template/public/manifest.json) which is [configurable](https://developer.chrome.com/extensions/manifest) by you to control what kind of extension you want build.

**Do not delete any of the entry files, this is a convention to remind you what your extensions could be. The build will notify you and fail if you remove any of these important files.**

## Creating a Browser Extension

**You’ll need to have Node 8.16.0 or Node 10.16.0 or later version on your local development machine** (but it’s not required on the server). You can use [nvm](https://github.com/creationix/nvm#installation) (macOS/Linux) or [nvm-windows](https://github.com/coreybutler/nvm-windows#node-version-manager-nvm-for-windows) to easily switch Node versions between different projects.

To create a new Browser Extension, you may choose one of the following methods:

### npx

```sh
npx create-react-app my-browser-extension --scripts-version react-browser-extension-scripts
```

_([npx](https://medium.com/@maybekatz/introducing-npx-an-npm-package-runner-55f7d4bd282b) comes with npm 5.2+ and higher, see [instructions for older npm versions](https://gist.github.com/gaearon/4064d3c23a77c74a3614c498a8bb1c5f))_

### npm

```sh
npm init react-app my-browser-extension --scripts-version react-browser-extension-scripts
```

_`npm init <initializer>` is available in npm 6+_

### Yarn

```sh
yarn create react-app my-browser-extension --scripts-version react-browser-extension-scripts
```

_`yarn create` is available in Yarn 0.25+_

It will create a directory called `my-browser-extension` inside the current folder.<br>
Inside that directory, it will generate the initial project structure and install the transitive dependencies:

```
my-browser-extension
├── README.md
├── node_modules
├── package.json
├── .gitignore
├── public
│   ├── img
│   │   ├── icon-16.png
│   │   ├── icon-48.png
│   │   ├── icon-128.png
│   ├── popup.html
│   └── manifest.json
└── src
    ├── background
    │   ├── index.js
    ├── contentScripts
    │   ├── index.js
    ├── App.css
    ├── App.js
    ├── App.test.js
    ├── index.css
    ├── index.js
    ├── logo.svg
```

No configuration or complicated folder structures, just the files you need to build your extension.<br>
Once the installation is done, you can open your project folder:

```sh
cd my-browser-extension
```

Inside the newly created project, you can run some built-in commands:

### `npm start` or `yarn start`

Runs the browser extension in development mode. You will see a `/dev` folder has been created in your project with the extension.<br>

To view the extension in your browser, [open up chrome and unpack extension](https://developer.chrome.com/extensions/getstarted#manifest).

The extension will automatically reload if you make changes to the code.<br>
You will see the build errors and lint warnings in the console.

<p align='center'>
<img src='https://cdn.rawgit.com/marionebl/create-react-app/9f62826/screencast-error.svg' width='600' alt='Build errors'>
</p>

### [`npm test` or `yarn test`](https://github.com/facebook/create-react-app#npm-test-or-yarn-test)

### `npm run build` or `yarn build`

Builds the app for production to the `build` folder.<br>
It correctly bundles React in production mode and optimizes the build for the best performance.

Your extension is ready to be shipped.

### [`npm run eject` or `yarn eject`](https://facebook.github.io/create-react-app/docs/available-scripts#npm-run-eject)

## Contributing

We'd love to have your helping hand on `create-react-extension`! See [CONTRIBUTING.md](CONTRIBUTING.md) for more information on what we're looking for and how to get started.

## Acknowledgements

We are grateful to everyone who has been a part of the following existing related projects for their ideas and collaboration:

- [Create-React-App](https://github.com/facebook/create-react-app)
- [How to Fork CRA Post](https://codeburst.io/customizing-create-react-app-done-right-4a22683f2e09) to help me create this successfully
- [React-chrome-extension-boilerplate](https://github.com/jhen0409/react-chrome-extension-boilerplate) and [create-chrome-extension](https://github.com/schovi/create-chrome-extension), both of unfortunately don't look like they're actively supported, but have been inspiration and shown an appetite for building extensions in the community.
- I have no doubt this will grow as the project grows.

## License

Create React App is open source software [licensed as MIT](https://github.com/VasilyShelkov/create-react-extension/blob/master/LICENSE).
