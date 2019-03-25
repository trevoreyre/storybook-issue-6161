# storybook-issue-6161

Reproduction of [Storybook issue 6161](https://github.com/storybooks/storybook/issues/6161), where installation of storybook v5 alongside create-react-app produces an error about incompatible webpack versions.

```bash
> react-scripts start


There might be a problem with the project dependency tree.
It is likely not a bug in Create React App, but something you need to fix locally.

The react-scripts package provided by Create React App requires a dependency:

  "webpack": "4.28.3"

Don't try to install it manually: your package manager does it automatically.
However, a different version of webpack was detected higher up in the tree:

  /Users/trevoreyre/storybook-issue-6161/node_modules/webpack (version: 4.29.6)
```

## Steps to reproduce

1. Create new app using `create-react-app`

```bash
create-react-app test-app
```

2. Install latest storybook (currently 5.0.5) using cli

```bash
cd test-app
npx -p @storybook/cli sb init
```

3. Move `react-scripts` in `package.json` to end of `devDependencies` list.

```json
{
  ...
  "dependencies": {
    "react": "^16.8.5",
    "react-dom": "^16.8.5"
  },
  "devDependencies": {
    "@storybook/react": "^5.0.5",
    "@storybook/addon-actions": "^5.0.5",
    "@storybook/addon-links": "^5.0.5",
    "@storybook/addons": "^5.0.5",
    "@babel/core": "^7.4.0",
    "babel-loader": "^8.0.5",
    "react-scripts": "2.1.8"
  }
  ...
}
```

4. Delete `node_modules` and `package-lock.json`, then run fresh `npm install`

5. Try running app with `npm start`
