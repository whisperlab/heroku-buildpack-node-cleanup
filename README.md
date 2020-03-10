# Heroku Buildpack: Node Cleanup

Make the official Heroku buildpack for Node.js compatible with other buildpacks

### Delete the node_modules and client/node_modules directories

The maximum allowed Heroku slug size (after compression) is 500MB (with 300MB soft limit). Image-heavy apps can somethings butt up against this limit, especially when using multiple buildpacks. If you're using Node.js to compile your front-end assets, but not to run your app, you may be able to save a large amount of space by deleting the `node_modules` directory before slug compilation.

## Usage

First, set the Node.js buildpack to compile your assets:

```bash
$ heroku buildpacks:set heroku/nodejs
```

Next, add whichever buildpack runs your app:

```bash
$ heroku buildpacks:set --index 1 heroku/ruby
```

Finally, add the Node Cleanup buildpack to get rid of the `node_modules` and `client/node_modules` directories:

```bash
$ heroku buildpacks:set --index 2 https://github.com/whisperlabs/heroku-buildpack-node-cleanup
```

## Documentation

For more general information about buildpacks on Heroku:

- [Using Multiple Buildpacks for an App](https://devcenter.heroku.com/articles/using-multiple-buildpacks-for-an-app)
- [Slug Compiler](https://devcenter.heroku.com/articles/slug-compiler)
