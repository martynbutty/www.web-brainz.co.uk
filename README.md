# Website

This website is built using [Docusaurus 2](https://docusaurus.io/), a modern static website generator.

## Installation

```console
yarn install
```
Note, to force a different registry (useful if you have an internal registry as your machine default), use the below. 
This will prevent your `yarn.lock` file referencing your internal registry which might not be accessible from all places
your trying to install from (e.g. if using AWS codeBuild)
```console
yarn --registry=https://registry.yarnpkg.com install
```

## Local Development

```console
yarn start
```

This command starts a local development server and opens up a browser window. Most changes are reflected live without having to restart the server.

## Build

```console
yarn build
```

This command generates static content into the `build` directory and can be served using any static contents hosting service.

## Deployment

```console
GIT_USER=<Your GitHub username> USE_SSH=true yarn deploy
```

If you are using GitHub pages for hosting, this command is a convenient way to build the website and push to the `gh-pages` branch.
