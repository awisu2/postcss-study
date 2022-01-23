# postcss

[postcss/postcss: Transforming styles with JS plugins](https://github.com/postcss/postcss)

- postcss って何？: css 専用 変換処理パッケージ, プラグインの付け足しで変換内容を決定できる
  - [軽く試してみた感じ](./gettingstart) css 版 ビルダー(webpack, Gulp, Grunt など) というのがイメージ
  - 非常に拡張性が高く、sass や stylus, Tailwind, autoprefixer などの有名どころにも対応。
    - というか、裏では利用しているというパターンもある
    - **各種フォーマットにプラグインの付け足しだけで対応可能**
- postCss は使うべきなのか？: 使えるなら使っておいたほうが楽になりそう
  - 最終出力は css なので、他の変換処理(loader や task)間に差し込める
- postcss.config.js を記載して pulugins に必要な拡張をセットするだけでほぼほぼ設定は完了
- vscode などエディタでのサポート拡張もある
- pluginsの実行順序、配列順におこなわれる

## ./docs

### 実例

- [gettingstart](./gettingstart): とりあえず触ってみる
- [samples](./samples): いくらか実用できそうな設定集

### document

- [postcss.conofig.js](./docs/postcss.config.js.md): postcss の設定ファイルについて
- [commands](./docs/commands.md): postcss コマンドまとめ
- [plugins](./plugins): プラグインまとめ

## 推奨記事

- [Some things you may think about PostCSS\.\.\. and you might be wrong \- Julian Ćwirko \- JavaScript and such](https://www.julian.io/articles/postcss.html)
- [It's Time for Everyone to Learn About PostCSS \| David Clark Develops the Web](https://davidtheclark.com/its-time-for-everyone-to-learn-about-postcss/)
- [PostCSS Deep Dive \- Envato Tuts\+ Web Design Tutorials](https://webdesign.tutsplus.com/series/postcss-deep-dive--cms-889)
