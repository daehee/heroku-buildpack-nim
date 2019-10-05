Heroku buildpack: Nim
=====================

This is a [Heroku buildpack](http://devcenter.heroku.com/articles/buildpacks)
for [Nim](http://nim-lang.org) apps. It uses
[Nimble](https://github.com/nim-lang/nimble) for dependency management.

Usage
-----

The buildpack expects you to include a `.nimble` file in order to
download dependencies and build your app.

Be sure to set the
[bin](https://github.com/nim-lang/nimble#binary-packages) value on
your nimble file to the executable name for your app.

You must also create a `release` nimble task to provide instructions
to this buildpack on how to compile your app. For example:

```nimble
task release, "Build a production release":
  --verbose
  --forceBuild:on
  --opt:speed
  --threads:on
  --define:release
  --define:ssl
  --hints:off
  --outdir:"."
  setCommand "c", "src/main.nim"
```

**Note:** Without this `task`, nimble will NOT be able to build your release.

Finally, create a `Procfile` with a process to run for your executable:

```yaml
web: ./main
```

Create an app using this buildpack

```shell
heroku create --buildpack https://github.com/OldhamMade/heroku-buildpack-nim.git
```

Example
-------

An [example nimble app](https://github.com/vic/nim-heroku-example)
lives [here](http://nim-heroku-example.herokuapp.com)
