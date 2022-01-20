# basic sampl

```bash
npm i

npm run build
# or
npm run dev
```

## settings

```bash
npm install postcss cssnano autoprefixer -D

# 環境変数設定
npm install cross-env -D

# 実行テストのためにインストール
npm install postcss-cli
```

_postcss.config.js_

```js
module.exports = {
  plugins: {
    autoprefixer: {},
    // 本番環境でminify
    ...(process.env.NODE_ENV === 'production' ? { cssnano: {} } : {})
  }
}
```

*pakcage.json*

```json
{...
  "scripts": {
    ...
    "dev": "postcss src/**/* -d dist -w",
    "build": "cross-env NODE_ENV=production postcss src/**/* -d dist"
  },
...}
```
