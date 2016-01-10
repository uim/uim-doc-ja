= uim-sh =

## これは何？ ##

対話型シェル。 [LibUim](LibUim.md)に内蔵されているSchemeのCLIを提供しています。

デバッグ用途などに使えます。

## 使い方 ##

ターミナルエミュレータなどからuim-shを起動します。

```
$ uim-sh
uim> (begin(display"Hello, uim!")(newline))
Hello, uim!
#<undef>
```

終了は

```
uim> (exit)
```

ファイルを直接読み込むこともできます。 パス指定は、絶対パスか/usr/local/share/uim/libディレクトリからの相対パスで。

```
$ uim-sh ~/hello.scm
```

更に[SRFI-22](http://srfi.schemers.org/srfi-22/)に従って引き数を渡せます。 ただし'''-e'''オプションが指定されている場合は無視されます。

```
$ uim-sh ~/cat.scm ~/foo.txt
```

Emacsから呼ぶ事もできます。 ~/.emacsに

```
(setq scheme-program-name "uim-sh")
```

と追記して、M-x run-schemeとしてください。

### オプション ###

  * -b, --batch:: バッチモードで起動します。プロンプトを表示しません。
  * -B, --strict-batch:: 厳密なバッチモードで起動します。プロンプトを表示せずに実行結果を評価します。
  * -r, --require-module ''モジュール名'':: モジュールを要求します。
  * --editline:: Emacs風の行編集のためにeditlineモジュールを要求します。このオプションを使うには、libeditサポートを有効にしてビルドする必要があります。
  * -e, --expression ''Scheme式'':: ''Scheme式''を評価します。
  * -V, --version:: ソフトウェアバージョンを表示します。
  * -h, --help:: ヘルプを表示します。