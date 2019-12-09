# Projects from demo

Demo application
- [npm-talk-app](https://github.com/jrhart08/npm-talk-app)

Demo packages
- [npm-talk-utils](https://github.com/jrhart08/npm-talk-utils) (vanilla npm versioning)
- [npm-talk-react-hooks](https://github.com/jrhart08/npm-talk-react-hooks) (using `standard-version`)
- [npm-talk-lerna](https://github.com/jrhart08/npm-talk-lerna) (using `lerna`)


Each of these projects (except the app) uses a different package publishing scheme.
View each one for more detailed documentation.

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
