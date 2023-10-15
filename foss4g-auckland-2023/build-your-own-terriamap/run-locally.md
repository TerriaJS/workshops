# Building & running Terria locally

This guide is adapted from https://docs.terria.io/guide/customizing/cloning-and-building/

## Guide

### Quickstart

If you've done this sort of thing before, you'll find it easy to clone and build TerriaMap with these quick instructions:

```bash
git clone https://github.com/TerriaJS/TerriaMap.git

cd TerriaMap

export NODE_OPTIONS=--max_old_space_size=4096

npm install -g yarn

yarn install && yarn gulp && yarn start

# Open at http://localhost:3001
```

If you run into trouble or want more explanation, read on.

### Prerequisites

TerriaJS can be built and run on almost any macOS, Linux, or Windows system. The following are required to build TerriaJS:

- The Bash command shell. On macOS or Linux you almost certainly already have this. On Windows, you can easily get it by installing [Git for Windows](https://gitforwindows.org/). In the instructions below, we assume you're using a Bash command prompt.
- [Node.js](https://nodejs.org) v14 or v16. You can check your node version by running `node --version` on the command-line.
- [npm](https://www.npmjs.com/) v6.0 or later. npm is usually installed automatically alongside the above. You can check your npm version by running `npm --version`.
- [yarn](https://yarnpkg.com/) v1.19.0 or later. This can be installed using `npm install -g yarn@^1.19.0`

### Cloning TerriaMap

The latest version of TerriaMap is on [GitHub](https://github.com), and the preferred way to get it is by using `git`:

```bash
git clone https://github.com/TerriaJS/TerriaMap.git

cd TerriaMap
```

If you're unable to use git, you can also [download a ZIP file](https://github.com/TerriaJS/TerriaMap/archive/main.zip) and extract it somewhere on your system. We recommend using git, though, because it makes it much easier to update to later versions in the future.

### Increase NodeJS memory limit

To avoid running out of memory when installing dependencies and building TerriaMap, increase the memory limit of node:

```bash
export NODE_OPTIONS=--max_old_space_size=4096
```

### Installing Dependencies

All of the dependencies required to build and run TerriaMap, other than the prerequisites listed above, are installed using `yarn`:

```bash
yarn install
```

The dependencies are installed in the `node_modules` subdirectory. No global changes are made to your system.

### Building TerriaMap

Do a standard build of TerriaMap with:

```bash
yarn gulp
```

Or, you can create a minified release build with:

```bash
yarn gulp release
```

To watch for changes and automatically do an incremental build when any are detected, use:

```bash
yarn gulp watch
```

The full set of `gulp` tasks can be found on the [Development Environment](https://docs.terria.io/guide/contributing/development-environment.md#terriamap-gulp-tasks) page.

### Running TerriaMap

TerriaMap includes a simple Node.js-based web server, called [terriajs-server](https://github.com/TerriaJS/terriajs-server). To start it, run:

```bash
yarn start
```

Then, open a web browser on `http://localhost:3001` to use TerriaMap.

## Troubleshooting

Checkout the [Problems and Solutions](https://docs.terria.io/guide/contributing/problems-and-solutions.md) page to see if we have them covered.

Here are some common ones:

### I have a newer version of NodeJS installed

You can use [nvm](https://github.com/nvm-sh/nvm#installing-and-updating) to manage multiple versions of NodeJS.

Follow installation instructions [here](https://github.com/nvm-sh/nvm#installing-and-updating).

Then run the following to install NodeJS v16 and use it:

```bash
nvm install 16
nvm use 16
```

### Install errors on M1/M2 macs

You may need to install Python2 to build NodeJS dependencies (like `node-sass`)

We recommend using [`pyenv`](https://github.com/pyenv/pyenv#installation) to install Python2.

Follow installation instructions [here](https://github.com/pyenv/pyenv#installation).

Then run the following to install Python 2.7.18 and use it:

```bash
pyenv install 2.7.18
pyenv shell 2.7.18
```
