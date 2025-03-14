# Bun Heroku Fir Cloud Native Buildpack

A cloud native buildpack to run bun on Heroku Fir.

## How to use

Add the buildpack to your `project.toml`

```
[[io.buildpacks.group]]
  id = "kilterset/bun"
  uri = "https://github.com/kilterset/heroku-bun-buildpack/releases/download/v0.0.2/buildpack-bun.cnb"
```

In order for your app to start correctly you will need to define either a start
script in `package.json` or a `Procfile` with a web process
e.g. (`web: bun src/app.js`).

If you have a build script defined in `package.json` it will be run as part of
the deployment.

If your have a release script defined in `package.json` a release process type
will be added so that this script is run after each deployment. You can override
this behavior with a `Procfile`.

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

# Packaging this buildpack for release

Run the following to package the buildpack
```
pack buildpack package buildpack-bun --format file
```

Once packaged tag and create a release in GitHub, be sure to include the
packaged buildpack (`buildpack-bun.cnb`) in the release.

Finally, update the readme to reference the url of the latest version to be used
in the `project.toml`.
