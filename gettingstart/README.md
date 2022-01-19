# gettingstart

cli、webpackでのサンプルを実装してみる

- cli: postcss-cliを利用したコマンドラインでの変換(コンフィグファイルの用意まで)
- webpack: webpackを利用した変換
- プラグイン: 利用したプラグインのリストとリンク
## cli

参考記事: [Getting started with PostCSS: A quick guide for Sass users \| by Svilen Gospodinov \| Heresy Dev \| Medium](https://medium.com/heresy-dev/getting-started-with-postcss-a-quick-guide-for-sass-users-90c8b675d5f4)

[postcss/postcss\-cli: CLI for postcss](https://github.com/postcss/postcss-cli)

### installと実行

```bash
npm init -y

npm install -D postcss-cli
npx postcss --help
```

*src/input.css*

変換元ファイル

```css
:fullscreen {
    color: red;
}
```

dist/output.cssに出力

```bash
npx postcss src/input.css -o dist/output.css
# 出力ディレクトリを指定(-o と -d は同時に指定できない)
npx postcss src/input.css -d dist
# 複数ファイルを指定することも可能
npx postcss src/*.css -d dist
npx postcss src/**/*.css -d dist
```

### sass相当の機能を付与

```bash
# 拡張機能のインストール
npm install -D postcss-import postcss-simple-vars postcss-nested postcss-mixins autoprefixer

# 有効にして変換(--use == -u)
npx postcss src/input.css -o dist/output.css --use autoprefixer postcss-import postcss-simple-vars postcss-nested postcss-mixins
```

### コンフィグファイルを利用して短縮

*postcss.config.js*

```js
module.exports = {
    plugins: [
        require('autoprefixer'),
        require('postcss-import'),
        require('postcss-simple-vars'),
        require('postcss-nested'),
        require('postcss-mixins'),
    ]
}
```

```bash
npx postcss src/input.css -o dist/output.css
```

## webpack

[Webpack \- Bootstrap 4\.4 \- 日本語リファレンス](https://getbootstrap.jp/docs/4.4/getting-started/webpack/#%E3%83%97%E3%83%AA%E3%82%B3%E3%83%B3%E3%83%91%E3%82%A4%E3%83%AB%E3%81%95%E3%82%8C%E3%81%9F-sass-%E3%81%AE%E3%82%A4%E3%83%B3%E3%83%9D%E3%83%BC%E3%83%88)

```bash
npm init -y

npm install webpack webpack-cli --save-dev
npm install --save lodash
```

## プラグイン

- [postcss/autoprefixer](https://github.com/postcss/autoprefixer): 各種ブラウザに対応する prefixを付与(例: -webkit, -ms)
- [postcss\-nested](https://github.com/postcss/postcss-nested): ネスト記載を有効化
- [postcss\-simple\-vars](https://github.com/postcss/postcss-simple-vars): 変数を有効化
- [postcss\-mixins](https://github.com/postcss/postcss-mixins): @mixinを有効化
- [postcss\-import](https://github.com/postcss/postcss-import): @importを有効化
