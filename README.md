## Setting environment

> Installing dependences

Run this commamnds with `yarn` or `npm` to manage the dependences.

Babel and webpack:

```
  yarn add @babel/core @babel/preset-env @babel/preset-react @babel/plugin-proposal-class-properties -D
  yarn add webpack webpack-cli -D
```

Webpack loaders:

```
  yarn add babel-loader style-loader css-loader file-loader -D
```

React lib:

```
  yarn add react react-dom
```

> Config babel

Create a file in root dir called `babel.config.js`:

```javascript
module.exports = {
  presets: ['@babel/preset-env', '@babel/preset-react']
};
```

> Config webpack

Create a file in root dir called `webpack.config.js`:

```javascript
const path = require('path');

module.exports = {
  entry: path.resolve(__dirname, 'src', 'index.js'),
  output: {
    path: path.resolve(__dirname, 'public'),
    filename: 'bundle.js'
  },
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: { loader: 'babel-loader' }
      },
      {
        test: /\.css$/,
        use: [{ loader: 'style-loader' }, { loader: 'css-loader' }]
      },
      {
        test: /.*\.(gif|jpe?g|png)$/i,
        use: { loader: 'file-loader' }
      }
    ]
  }
};
```

To run the build:

```
  webpack --mode development
```

## Auto reload application

```
  yarn add webpack-dev-server -D
```

Change webpack config, adding a `devServer` prop:

```javascript
const path = require('path');

module.exports = {
  entry: path.resolve(__dirname, 'src', 'index.js'),
  output: {
    path: path.resolve(__dirname, 'public'),
    filename: 'bundle.js'
  },
  devServer: {
    contentBase: path.resolve(__dirname, 'public')
  },
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: { loader: 'babel-loader' }
      }
    ]
  }
};
```

Now to build app, just run:

```
  webpack-dev-server --mode development
```
