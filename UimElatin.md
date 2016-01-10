= uim-elatin =



## これは何？ ##

Emacsスタイルのラテン文字入力方式。

## 使い方 ##

  1. [UimImSwitcher](UimImSwitcher.md)や[UimToolbar](UimToolbar.md)からELatinに切り換えてください。
    1. ELatinが見つからない場合は[UimPref](UimPref.md)を起動してください。
      * [UimToolbar](UimToolbar.md)の設定アイコンをクリック
      * ターミナルエミュレータなどでuim-pref-gtk（もしくはuim-pref-qt）を実行
    1. 起動したら、「全体設定」→「入力方式の利用準備」→「使用可能にする入力方式」の「編集...」ボタンを押して、左の有効アイテムにELatinを追加してください。
      * そこにもELatinが見つからない場合、uim-elatinはインストールされていないのかもしれません。確認してみてください。
    1. 追加が完了したら、ELatinで入力したいアプリケーションを再起動してください。
  1. [UimImSwitcher](UimImSwitcher.md)や[UimToolbar](UimToolbar.md)による切り換えは一時的なものです。永続的な変更を望むなら[UimPref](UimPref.md)で設定する必要があります。
  1. [UimPref](UimPref.md)を起動したら、「全体設定」→「入力方式の利用準備」→「標準の入力方式を指定」のチェックボックスにチェックを入れます。
  1. そのすぐ下の「標準の入力方式」に、ELatinをセットしてください。

### 標準で指定されているキー設定 ###

| 動作 | キー |
|:---|:---|
| オン/オフ | Ctrl+\ |
| カーソルの左の一字を削除 | BS、Ctrl+h |

### ファイル ###

~/.uim.d/custom/custom-elatin.scm:: [UimPref|UimPref]の「ELatin」ファイル。

## カスタマイズ可能な項目 ##

### Elatinの変数 ###

| 動作 | 変数名 | 指定できる値 | 標準値 |
|:---|:----|:-------|:----|
| ラテン文字のキーボード配列 | elatin-rules | 'elatin-rules-latin-prefix<br> 'elatin-rules-british<br> 'elatin-rules-catalan-prefix<br> 'elatin-rules-danish-postfix<br> 'elatin-rules-danish-alt-postfix<br> 'elatin-rules-danish-keyboard<br> 'elatin-rules-dutch<br> 'elatin-rules-english-dvorak<br> 'elatin-rules-esperanto-prefix<br> 'elatin-rules-esperanto-postfix<br> 'elatin-rules-esperanto-alt-postfix<br> 'elatin-rules-finnish-postfix<br> 'elatin-rules-finnish-alt-postfix<br> 'elatin-rules-finnish-keyboard<br> 'elatin-rules-french-prefix<br> 'elatin-rules-french-postfix<br> 'elatin-rules-french-alt-postfix<br> 'elatin-rules-french-keyboard<br> 'elatin-rules-french-azerty<br> 'elatin-rules-german-prefix<br> 'elatin-rules-german-postfix<br> 'elatin-rules-german-alt-postfix<br> 'elatin-rules-german<br> 'elatin-rules-icelandic-postfix<br> 'elatin-rules-icelandic-alt-postfix<br> 'elatin-rules-icelandic-keyboard<br> 'elatin-rules-irish-prefix<br> 'elatin-rules-italian-postfix<br> 'elatin-rules-italian-alt-postfix<br> 'elatin-rules-italian-keyboard<br> 'elatin-rules-latin-prefix<br> 'elatin-rules-latin-postfix<br> 'elatin-rules-latin-alt-postfix<br> 'elatin-rules-latin-1-prefix<br> 'elatin-rules-latin-1-postfix<br> 'elatin-rules-latin-1-alt-postfix<br> 'elatin-rules-latin-2-prefix<br> 'elatin-rules-latin-2-postfix<br> 'elatin-rules-latin-2-alt-postfix<br> 'elatin-rules-latin-3-prefix<br> 'elatin-rules-latin-3-postfix<br> 'elatin-rules-latin-3-alt-postfix<br> 'elatin-rules-latin-4-postfix<br> 'elatin-rules-latin-4-alt-postfix<br> 'elatin-rules-latin-5-postfix<br> 'elatin-rules-latin-5-alt-postfix<br> 'elatin-rules-latin-8-prefix<br> 'elatin-rules-latin-9-prefix<br> 'elatin-rules-latvian-keyboard<br> 'elatin-rules-lithuanian-keyboard<br> 'elatin-rules-lithuanian-numeric<br> 'elatin-rules-norwegian-postfix<br> 'elatin-rules-norwegian-alt-postfix<br> 'elatin-rules-norwegian-keyboard<br> 'elatin-rules-polish-slash<br> 'elatin-rules-portuguese-prefix<br> 'elatin-rules-romanian-prefix<br> 'elatin-rules-romanian-alt-prefix<br> 'elatin-rules-scandinavian-postfix<br> 'elatin-rules-scandinavian-alt-postfix<br> 'elatin-rules-slovenian<br> 'elatin-rules-spanish-prefix<br> 'elatin-rules-spanish-postfix<br> 'elatin-rules-spanish-alt-postfix<br> 'elatin-rules-spanish-keyboard<br> 'elatin-rules-swedish-postfix<br> 'elatin-rules-swedish-alt-postfix<br> 'elatin-rules-swedish-keyboard<br> 'elatin-rules-turkish-postfix<br> 'elatin-rules-turkish-alt-postfix<br> 'elatin-rules-turkish-latin-3-postfix<br> 'elatin-rules-turkish-latin-3-alt-postfix <table><thead><th> 'elatin-rules-latin-prefix </th></thead><tbody>
<tr><td> ESCキーでラテン文字入力モードをオフにする (viユーザ向け) </td><td> elatin-esc-turns-off? </td><td> #t #f  </td><td> #f  </td></tr></tbody></table>

<h3>ELatinキー設定の変数</h3>

<table><thead><th> 動作 </th><th> キー変数名 </th></thead><tbody>
<tr><td> オン </td><td> elatin-on-key? </td></tr>
<tr><td> オフ </td><td> elatin-off-key? </td></tr>
<tr><td> バックスペース </td><td> elatin-backspace-key? </td></tr>