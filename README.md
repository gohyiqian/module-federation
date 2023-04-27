# Micro-Frontend Architecture

## Module Federation

- Introduces in Webpack 5
- We can share bundles across 2 standalone applications that run separately

## Exposes

- Hello World App running on 9001

```js
  output: {
    filename: '[name].[contenthash].js',
    path: path.resolve(__dirname, './dist'),
    // update public path
    publicPath: 'http://localhost:9001/',
  },
// ...
  plugins: [
     new ModuleFederationPlugin({
      name: 'HelloWorldApp',
      filename: 'remoteEntry.js',
      exposes: {
        './HelloWorldButton':
          './src/components/hello-world-button/hello-world-button.js',
      },
    }),
  ],

```

## Remotes

- Kiwi App running on 9002

```js
  plugins: [
    new ModuleFederationPlugin({
      name: 'KiwiApp',
      remotes: {
        HelloWorldApp: 'HelloWorldApp@http://localhost:9001/remoteEntry.js',
      },
    }),
  ],

```
