# vue-starter

This is vue starter repository without vue-cli

This This vue starter consists of **eslint**, **prettier**, **webpack**.

# How to ?

## install

```
> mkdir vue-test
> cd vue-test
> npm init -y       // To your liking options

> npm i vue
> npm i -D @babel/core @babel/preset-env babel-loader css-loader eslint eslint-config-prettier eslint-plugin-prettier eslint-plugin-vue html-webpack-plugin vue-loader vue-style-loader vue-template-compiler webpack webpack-cli webpack-dev-server
```

> @babel/core, @babel/preset-env : Convert ES6 code to ES5 code

> babel-loader : Convert ES6 code to ES5 code (Need help with dependencies between @ babel / core and @ babel / preset-env)

> webpack : Necessary for bundling

> webpack-cli :
> Needed to run Webpack command

> webpack-dev-server : Tools useful when developing locally

> vue-loader :
> Converts vue files to JavaScript files when bundled in Webpack

> css-loader :
> Get the CSS you've written into the .vue file or the CSS you want to import into the JavaScript file and check the path to that file.

> vue-style-loader :
> Insert CSS imported into css-loader into an HTML file. This creates and inserts a style tag in the header part of the HTML document.

> eslint, eslint-plugin-vue, eslint-plugin-prettier, eslint-config-prettier : Files needed for eslint & prettier setup

> html-webpack-plugin : Take index.html and insert the bundled JavaScript file into the header. Then copy to dist folder

> vue-template-compiler : Converts vue files to JavaScript files when bundled in Webpack

## .babelrc.js

```
module.exports = {
  presets: ['@babel/preset-env'],
};

```

## .eslintrc.js

```
module.exports = {
  root: true,
  extends: [
    'eslint:recommended',
    'plugin:vue/essential',
    'prettier',
    'plugin:prettier/recommended',
  ],
  plugins: ['prettier'],
  rules: {
    'prettier/prettier': [
      'error',
      {
        ... Set rules you want to set
      },
    ],
    'no-console': process.env.NODE_ENV === 'production' ? 'error' : 'off',
  },
};

```

## .eslintignore

```
/node_modules/*
webpack.config.js

```

## webpack.config.js

```
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');
const VueLoaderPlugin = require('vue-loader/lib/plugin');
const webpack = require('webpack');

module.exports = {
  mode: 'development',
  devtool: 'eval',
  resolve: {
    extensions: ['.js', '.vue'],
    alias: {
      '@': path.resolve(__dirname, 'src'),
    },
  },
  entry: './src/main.js',
  module: {
    rules: [
      {
        test: /\.js$/,
        use: 'babel-loader',
      },
      {
        test: /\.vue$/,
        use: 'vue-loader',
      },
      {
        test: /\.css$/,
        use: ['vue-style-loader', 'css-loader'],
      },
    ],
  },
  devServer: {
    open: true,
    hot: true,
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: './public/index.html',
    }),
    new VueLoaderPlugin(),
    new webpack.HotModuleReplacementPlugin(),
  ],
};


```
