# gettingstart

cli、webpack でのサンプルを実装してみる

- cli: postcss-cli を利用したコマンドラインでの変換(コンフィグファイルの用意まで)
- webpack: webpack を利用した変換
- プラグイン: 利用したプラグインのリストとリンク

## cli

参考記事: [Getting started with PostCSS: A quick guide for Sass users \| by Svilen Gospodinov \| Heresy Dev \| Medium](https://medium.com/heresy-dev/getting-started-with-postcss-a-quick-guide-for-sass-users-90c8b675d5f4)

[postcss/postcss\-cli: CLI for postcss](https://github.com/postcss/postcss-cli)

### install と実行

```bash
npm init -y

npm install -D postcss-cli
npx postcss --help
```

_src/input.css_

変換元ファイル

```css
:fullscreen {
  color: red;
}
```

dist/output.css に出力

```bash
npx postcss src/input.css -o dist/output.css
# 出力ディレクトリを指定(-o と -d は同時に指定できない)
npx postcss src/input.css -d dist
# 複数ファイルを指定することも可能
npx postcss src/*.css -d dist
npx postcss src/**/*.css -d dist
```

### sass 相当の機能を付与

```bash
# プラグインのインストール
npm install -D postcss-import postcss-simple-vars postcss-nested postcss-mixins autoprefixer

# 有効にして変換(--use == -u)
npx postcss src/input.css -o dist/output.css --use autoprefixer postcss-import postcss-simple-vars postcss-nested postcss-mixins
```

### コンフィグファイルを利用して短縮

_postcss.config.js_

```js
module.exports = {
  plugins: [
    require('autoprefixer'),
    require('postcss-import'),
    require('postcss-simple-vars'),
    require('postcss-nested'),
    require('postcss-mixins')
  ]
}
```

```bash
npx postcss src/input.css -o dist/output.css
```

## webpack

- [Webpack \- Bootstrap 4\.4 \- 日本語リファレンス](https://getbootstrap.jp/docs/4.4/getting-started/webpack/#%E3%83%97%E3%83%AA%E3%82%B3%E3%83%B3%E3%83%91%E3%82%A4%E3%83%AB%E3%81%95%E3%82%8C%E3%81%9F-sass-%E3%81%AE%E3%82%A4%E3%83%B3%E3%83%9D%E3%83%BC%E3%83%88)
- [webpack\-contrib/postcss\-loader: PostCSS loader for webpack](https://github.com/webpack-contrib/postcss-loader)

```bash
npm init -y

npm install -D webpack webpack-cli
npm install -D style-loader css-loader postcss-loader

# プラグインのインストール
npm install -D postcss-import postcss-simple-vars postcss-nested postcss-mixins autoprefixer
```

### ファイルの用意

_src/input.css_

```css
$c: red;

:fullscreen {
  color: $c;
}

* {
  color: $c;
}
```

_index.js_

webpack の起点ファイル

```js
import './input.css'
```

_webpack.config.js_

```js
const path = require('path')

module.exports = {
  entry: './src/index.js',
  output: {
    filename: 'main.js',
    path: path.resolve(__dirname, 'dist')
  },
  mode: 'none',
  resolve: {
    extensions: ['.js']
  },
  module: {
    rules: [
      {
        test: /\.css$/,
        exclude: /node_modules/,
        use: [
          {
            loader: 'style-loader'
          },
          {
            loader: 'css-loader',
            options: {
              importLoaders: 1
            }
          },
          {
            loader: 'postcss-loader'
          }
        ]
      }
    ]
  }
}
```

_postcss.config.js_

postcss の設定、webpack.config.js に直接記載することも可能([webpack\-contrib/postcss\-loader: PostCSS loader for webpack](https://github.com/webpack-contrib/postcss-loader))

```js
module.exports = {
  plugins: [
    require('autoprefixer'),
    require('postcss-import'),
    require('postcss-simple-vars'),
    require('postcss-nested'),
    require('postcss-mixins')
  ]
}
```

_index.html_

確認用 html

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>

  <body>
    hello world

    <script src="./dist/main.js"></script>
  </body>
</html>
```

### 変換

```bash
npx webpack
```

先程の index.html を開くと文字が赤くなっている

## プラグイン

- [postcss/autoprefixer](https://github.com/postcss/autoprefixer): 各種ブラウザに対応する prefix を付与(例: -webkit, -ms)
- [postcss\-nested](https://github.com/postcss/postcss-nested): ネスト記載を有効化
- [postcss\-simple\-vars](https://github.com/postcss/postcss-simple-vars): 変数を有効化
- [postcss\-mixins](https://github.com/postcss/postcss-mixins): @mixin を有効化
- [postcss\-import](https://github.com/postcss/postcss-import): @import を有効化
