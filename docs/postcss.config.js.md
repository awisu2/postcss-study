# postcss.coonfig.js

コマンド実行時に実行されるconfigファイルの詳細

```js
module.exports = (ctx) => ({
    parser: 'sugarss',
    plugins: [
        require('autoprefixer'),
        require('postcss-import'),
        require('postcss-simple-vars'),
        require('postcss-nested'),
        require('postcss-mixins'),
    ]
})
```

## parser

[postcss/postcss: Transforming styles with JS plugins](https://github.com/postcss/postcss#syntaxes)

## ctx について

対象ファイルごとのパラメータがセットされ、config値をカスタマイズできる

[postcss/postcss\-cli: CLI for postcss](https://github.com/postcss/postcss-cli#context)
