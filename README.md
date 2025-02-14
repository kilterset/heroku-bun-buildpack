# Bun Heroku Fir Cloud Native Buildpack

A cloud native buildpack to run bun on Heroku Fir.

## How to use

In order for your app to start correctly you will need to define either a start
script in `package.json` or a `Procfile` with a web process
e.g. (`web: bun src/app.js`).

## Installing a specific Bun version

There are two options for pinning a specific version to install;
1. Create a file (`.bun-version`) at the root of the project

    `.bun-version`
    ```
    1.2.2
    ```

2. Provide a build time environment variable (`BUN_VERSION`) containing the version

    `project.toml`
    ```
    [[io.buildpacks.build.env]]
      name = "BUN_VERSION"
      value = "1.2.2"
    ```

    Or, when building locally

    ```
    pack build --builder heroku/builder:24 --env BUN_VERSION=1.2.2 my-app
    ```
