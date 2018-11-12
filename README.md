# Sample repo for TSLint issue #3980

The purpose of this repo is to show an example use case that produces the issue `no-implicit-dependencies: make nested package check optional #3980` from the TSLint github repo.

Using nested package.json files to create import shortcuts is a pretty common setup in react-native projects. People creates package.json files with just a name on it to avoid deeply nested relative path transversal, ex: ../../../../redux/selectors/user. The metro packager supports it by default without any configuration.

In this repo such a file can be found at `very/deeply/nested/package.json`, and an example usage of the shortcut import in `App.js`

The provided configuration for `eslint` is able to lint the dependencies for the sample JS file in the `very/deeply/nested` folder, but the `tslint` configuration fails with the following errors:

```
yarn run v1.12.1
$ tslint --project tsconfig.json

ERROR: /Users/elyalvarado/Workspace/World/TSLintFailingSample/very/deeply/nested/tslint_sample.tsx[1, 19]: Module 'react' is not listed as dependency in package.json
ERROR: /Users/elyalvarado/Workspace/World/TSLintFailingSample/very/deeply/nested/tslint_sample.tsx[2, 22]: Module 'react-native' is not listed as dependency in package.json
```

Note that in both cases the `@nested` prefix is excluded from the rules because it won't be resolved by `tslint` or `eslint` (however is properly resolved by the `metro` packager of react-native).

## Lintint the project

To lint the javascript files run: `yarn eslint`

To lint the typescript files run: `yarn tslint`
