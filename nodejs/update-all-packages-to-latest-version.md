# Update all packages to latest version

You can use [npm-check-updates](https://www.npmjs.com/package/npm-check-updates) to upgrade dependencies in `package.json` to the _latest_ version.

Show any new dependencies for the project:

```bash
npx npm-check-updates
```

Upgrade all dependencies:

```bash
npx npm-check-updates -u
```

The command modifies `package.json`, but _does not_ run the installation command. Follow up with `npm install` or whatever package manager you use.

[Read more about how dependency updates are determined](https://github.com/raineorshine/npm-check-updates#how-dependency-updates-are-determined).

You can also run [Doctor Mode](https://github.com/raineorshine/npm-check-updates#doctor-mode) to run tests will upgrading.
