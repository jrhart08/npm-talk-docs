# Verdaccio

## Description

A free and easy-to-use NPM registry for hosting your private packages.

It can be installed as an npm package or a docker image. We're just going to use npm here.

Read more here:
  - https://verdaccio.org/en/
  - https://github.com/verdaccio/verdaccio

## Setup

Run these (in order) from anywhere

```bash
# yes, install globally
# do it
# feel the power of the dark side flow through you
npm i -g verdaccio

# start verdaccio server
# (default: http://localhost:4873)
verdaccio

# setup registry key
# the auth token will be added to $HOME/.npmrc
# verdaccio uses this .npmrc too
# put the token in your project's .npmrc if you'd like
npm adduser --registry=http://localhost:4873
```

# Setting up your private package
In `~/path/to/your-package/.npmrc`

```
@jrh:registry=http://localhost:4873
//localhost:4873/:_authToken="{the token found in $HOME/.npmrc}"
```

In `~/path/to/your-package/package.json`

```json
{
  "name": "@jrh/your-project"
}
```

# `standard-version`

## Description

`standard-version` automates version and CHANGELOG  by looking at git commit messages.

  - For instance, if any commit message since its last release starts with `feat:`, it will do a minor version bump (e.g. `v1.2.3 -> v1.3.0`).

More detailed docs [here](https://www.npmjs.com/package/standard-version).

## Usage
From `~/path/to/your-project/`

```bash
npm i -D standard-version
```

In `~/path/to/your-project/package.json`

```json
{
  "scripts": {
    "release": "standard-version"
  }
}
```

From `~/path/to/your-project/`

```bash
npm run release
```

That's it!
  - It works by (git) tagging releases.
  - When you run it, it looks at all commits since the last tagged release.

**NOTE:** This can be part of your CI pipeline! Our team's CI script runs `npm run release` (just like this) after each merge into `master`

# Lerna

## Description

Popular tool for managing multiple npm packages in 1 git repo.

Used in projects like Babel, React, Angular, and Storybook.

Read more here:
  - https://lerna.js.org/
  - https://github.com/lerna/lerna

## Usage

In `~/path/to/your-project/` (If starting from scratch)

```bash
# Will initialize the following files/folders:
# lerna.json
# package.json
# packages/
npx lerna init
```

Add to `~/path/to/your-project/.npmrc` (if applicable)

```
@jrh:registry=http://localhost:4873
//localhost:4873/:_authToken="{the token found in $HOME/.npmrc}"
```

Create a package

```bash
# `-y` skips all those `npm init` prompts for name, version, description, etc
# version will default to the version in lerna.json
npx lerna create @jrh/my-first-lerna-package -y
```

**IMPORTANT:** Run this whenever you add a reference from one package to another.

```bash
# npm-links each package under `packages/` together
npx lerna bootstrap
```
