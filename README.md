# inline-glsl-compress-loader

A very simple webpack loader that reduces size of inline `glsl` fragments by appropriately removing spaces, new-lines and comments. These fragments must start with a comment `//glsl` so that it can be easily detected<sup>[1](#1)</sup>. Significant file size gain for important WebGL applications.

## Getting Started

### Installation


```shell
  npm install --save-dev inline-glsl-compress-loader
```

or

```shell
  yarn add --dev inline-glsl-compress-loader
```

### Usage

In your webpack config file, add the loader before other loaders:
```javascript
  {
    loader: 'inline-glsl-compress-loader'
  }
```
for the script files that needs it. For instance, it can be `.js` files, `.vue` files, etc.:
```javascript
  // webpack config
  // ...
  module: {
    rules: [
      {
        test: /\.vue$/,
        use: [{
          loader: 'vue-loader',
          options: vueLoaderConfig
        },
        {
          loader: 'inline-glsl-compress-loader'
        },
        ]
      },
      // other rules
      // ...
    }
    // ...
  }
```

### Example

This `js` sample code:

```javascript
  var vertexShader = compileShader(`//glsl
    attribute vec2 position;
    void main() {
        // this is a comment
        gl_Position = vec4(position, 0.0, 1.0);
    }
  `, gl.VERTEX_SHADER);
```

will be compressed into:

```javascript
  var vertexShader = compileShader(`attribute vec2 position;void main() {gl_Position = vec4(position, 0.0, 1.0);}`, gl.VERTEX_SHADER);
```

## Contributing
Feel free to contribute to this project

## License
Copyright (c) 2018 François Risoud
Licensed under the MIT license.

# 

#### Notes

<a name="1">1</a> - I use also this comment for my syntax highlighter to detect `glsl` fragments.
