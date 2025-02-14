# Webpack WAR plugin

Update the plugin to work with webpack 5

## WEBPACK 5 COMPATIBLE

## FORK FROM [DevWurm/webpack-war-plugin](https://github.com/DevWurm/webpack-war-plugin)

## Installation

You can install the plugin via npm

```bash
npm install --dev webpack-war-plugin
```

## Usage

### Basic Usage

To add the webpack-war-plugin to your build just add an instance of `WebpackWarPlugin` to the `plugins` section of your Webpack configuration

```javascript
const { WebpackWarPlugin } = require('webpack-war-plugin');

module.exports = {
  ...,
  plugins: [
    new WebpackWarPlugin(),
    ...
  ],
  ...
};
```

By default an archive containing all emitted Webpack build outputs is generated in the output directory of your Webpack build. It is named like your project.

### Configuration

You can influence the generated archive by supplying a configuration object of the following structure to the plugins constructor:

```typescript
type WebpackWarPluginOptions = {
  archiveName?: string;
  webInf?: string;
  additionalElements?: {
    path: string;
    destPath?: string;
  }[];
  archiverOptions?: {};
};
```

| Option                            | Effect                                                                                                                                                                                                                                                                                                |
| --------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `archiveName` _[optional]_        | Sets the output name of the archive                                                                                                                                                                                                                                                                   |
| `webInf` _[optional]_             | Specifies a path to a directory (or file) which will be included into the archive with the path `WEB-INF`                                                                                                                                                                                             |
| `additionalElements` _[optional]_ | Specifies multiple files or directories, which will be included in the archive. Each entry is a object with the following properties: `path` (The path of the source element), `destPath` (_[optional]_ The path of the specified file / directory inside of the archive [by default `path` is used]) |
| `archiverOptions` _[optional]_    | Specifies the options that should be used by `archiver` (used to create the archive). See https://archiverjs.com/docs/ for more information.                                                                                                                                                          |

### Example

The following plugin configuration:

```javascript
const { WebpackWarPlugin } = require('webpack-war-plugin');

module.exports = {
  entry: {
    file1: './src/file1.js'
  },
  ...,
  plugins: [
    new WebpackWarPlugin({
      archiveName: 'archive',
      webInf: './web-inf',
      additionalElements: [
        { path: 'context/context.xml', destPath: 'META-INF/context.xml'},
        { path: 'package.json' },
        { path: 'images', destPath: 'assets/images' }
      ],
      archiverOptions: {
        zlib: {
          level: 9
        }
      }
    }),
    ...
  ],
  ...
};

```

generates an archive with the name `archive.war` in the Webpack output directory with the following structure:

```
archive.war
|
|\_ file1.js
|
|\_ WEB-INF
|          \_ web.xml
|
|\_ META-INF
|           \_ context.xml
|
|\_ package.json
|
 \_ assets
          \_ images
                   \_ img.png
```

## Development

### Typescript

The plugin is built with [Typescript](http://www.typescriptlang.org/) and the resulting package contains the corresponding typings.

### Building

After checking out the project you can build transpile the Typescript via

```bash
npm run build
```

The build output is stored in `dist`.

### Testing

#### Unit tests

Unit tests are named `[tested-component].spec.ts`.<br>
They can be run via [Mocha](https://mochajs.org/) with

```bash
npm run test
```

Test coverage is measured via [nyc](https://github.com/istanbuljs/nyc) and can be triggered with

```bash
npm run test:coverage
```

#### Functional tests

Functional test fixtures are located in `functional_tests`.
To set up all fixtures run

```bash
npm run test:functional:setup
```

To execute the tests via Mocha run

```bash
npm run test:functional
```

### Continuous integration

Continious integration is realized via [Travis-CI](https://travis-ci.org/DevWurm/webpack-war-plugin). Coverage reports are shown on [Coveralls](https://coveralls.io/github/DevWurm/webpack-war-plugin). Deployments to NPM are automatically triggered via Git tags.

## Licensing

The app is distributed under the MIT License (read [`LICENSE`](LICENSE) for more information).
Copyright (c) 2017 Leo Lindhorst

## Collaborating

I really appreciate any kind of collaboration!<br>
You can use the [GitHub issue tracker](https://github.com/DevWurm/webpack-war-plugin/issues) for bugs and feature requests or [create a pull request](https://github.com/DevWurm/webpack-war-plugin/pulls) to submit
changes.
If you don't want to use these possibilities, you can also write me an email to
<a href='mailto:devwurm@devwurm.net'>devwurm@devwurm.net</a>.

## Contact

If you have any questions, ideas, etc. feel free to contact me:<br>
DevWurm<br>
Email: <a href='mailto:devwurm@devwurm.net'>devwurm@devwurm.net</a><br>
Jabber: devwurm@conversations.im<br>
Twitter: [@DevWurm](https://twitter.com/DevWurm)<br>
