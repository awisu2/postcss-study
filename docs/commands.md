# commands

- base: `npx postcss input.css -d dist`
  - 複数ファイルを対象とする: `npx postcss ./**/*.css ./**/*.html -d dist`
- 出力先: `-d` or `-o`
  - -d と -o は同時に指定できない
  - `-d`: 出力先ディレクトリ、input が複数の場合はこちら
  - `-o`: 出力先ファイル、出力ファイル名の指定が可能
- watch: `-w` or `--watch` ファイル更新時に反応、新規ファイル追加時には反応しなかった
