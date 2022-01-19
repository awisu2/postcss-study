# postcss.coonfig.js

コマンド実行時に実行される config ファイルの詳細

```js
module.exports = (ctx) => ({
  parser: 'sugarss',
  plugins: [
    require('autoprefixer'),
    require('postcss-import'),
    require('postcss-simple-vars'),
    require('postcss-nested'),
    require('postcss-mixins')
  ]
})
```

## parser

[postcss/postcss: Transforming styles with JS plugins](https://github.com/postcss/postcss#syntaxes)

特定の形式のファイルを変換対象にできる

- 例えば `postcss-html` をセットすると、`<style>` タグ内の css を対象に処理ができる
  - `sugarss`: Sass や Stylus などのインデントベース形式を対象
- require は記載しないがこれらも利用する場合はインストールする必要あり

### todo

- [] 複数記載できないのでこれをセットしたときの制限などは別途調査の必要あり

## ctx について

対象ファイルごとのパラメータがセットされ、config 値をカスタマイズできる

[postcss/postcss\-cli: CLI for postcss](https://github.com/postcss/postcss-cli#context)
