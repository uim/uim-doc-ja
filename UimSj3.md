= uim-sj3 =



## これは何？ ##

uimの[SJ3](http://code.google.com/p/sj3/)モジュール。 連文節かな漢字変換エンジンSJ3で入力/変換などを行なう場合に使う。

このモジュールは標準では含まれません。 '''--with-sj3'''をつけてuimをコンパイルする必要があります。

## 使い方 ##

  1. あらかじめSJ3サーバを起動しておいてください。
  1. [UimImSwitcher](UimImSwitcher.md)や[UimToolbar](UimToolbar.md)からSJ3に切り換えてください。
    1. SJ3が見つからない場合は[UimPref](UimPref.md)を起動してください。
      * [UimToolbar](UimToolbar.md)の設定アイコンをクリック
      * ターミナルエミュレータなどでuim-pref-gtk（もしくはuim-pref-qt）を実行
    1. 起動したら、「全体設定」→「入力方式の利用準備」→「使用可能にする入力方式」の「編集...」ボタンを押して、左の有効アイテムにSJ3を追加してください。
      * そこにもSJ3が見つからない場合、uim-sj3はインストールされていないのかもしれません。確認してみてください。
    1. 追加が完了したら、SJ3で入力したいアプリケーションを再起動してください。
  1. [UimImSwitcher](UimImSwitcher.md)や[UimToolbar](UimToolbar.md)による切り換えは一時的なものです。永続的な変更を望むなら[UimPref](UimPref.md)で設定する必要があります。
  1. [UimPref](UimPref.md)を起動したら、「全体設定」→「入力方式の利用準備」→「標準の入力方式を指定」のチェックボックスにチェックを入れます。
  1. そのすぐ下の「標準の入力方式」に、SJ3をセットしてください。

### サポートしている入力モード ###

  * 直接(無変換)入力モード
  * ひらがな入力モード
  * カタカナ入力モード
  * 半角カタカナ入力モード
  * 半角英数入力モード
  * 全角英数入力モード

### サポートしているかな入力方式 ###

  * [ローマ字入力方式](RomaKanaTable.md)
  * [AZIK拡張ローマ字入力方式](AZIKTable.md)
  * ACT拡張ローマ字入力方式
  * KZIK拡張ローマ字入力方式
  * かな入力方式

### 標準で指定されているキー設定 ###

| 動作 | キー |
|:---|:---|
| オン/オフ | 全角/半角、Shift+Space |
| ひらがな入力モードへ | Shift+F6 |
| カタカナ入力モードへ | Shift+F7 |
| 半角カタカナ入力モードへ | Shift+F8 |
| 全角英数入力モードへ | Shift+F9 |
| 半角英数入力モードへ | Shift+F10 |
| カーソルを右へ移動 | →、Ctrl+f |
| カーソルを左へ移動 | ←、Ctrl+b |
| 編集領域の先頭へ移動 | Home、Ctrl+a |
| 編集領域の末尾へ移動 | End、Ctrl+e |
| カーソルより右の文字をすべて削除 | Ctrl+k |
| カーソルより左の文字をすべて削除 | Ctrl+u |
| カーソルの右の一字を削除 | Delete、Ctrl+d |
| カーソルの左の一字を削除 | BS、Ctrl+h |
| 変換開始 | Space |
| 文節を伸ばす | Shift+→、Ctrl+o |
| 文節を縮める | Shift+←、Ctrl+i |
| 次の変換候補へ移動 | Space、↓、Ctrl+n |
| 前の変換候補へ移動 | ↑、Ctrl+p |
| 候補ウィンドウを次のページへ移動 | PgDn |
| 候補ウィンドウを次のページへ移動 | PgUp |
| 次の文節へ移動 | →、Ctrl+f |
| 前の文節へ移動 | ←、Ctrl+b |
| 変換確定 | Return、Ctrl+m、Ctrl+j |
| キャンセル | Esc、Ctrl+[、Ctrl+g |
| ひらがなへ変換 | F6 |
| カタカナへ変換 | F7 |
| 半角カタカナへ変換 | F8 |
| 全角英数字へ変換、大文字小文字を反転 | F9 |
| 半角英数字へ変換、大文字小文字を反転 | F10 |
| ひらがな、カタカナ、半角カタカナへの変換を循環 | 無変換 |

### 日本語と英語の交ぜ書き変換をする ###

入力中（編集領域が表示されている状態）で設定したキーを押すと、入力中の文字列を確定せず、ひらがな入力モードと半角英数入力モード、半角カタカナモードと全角英数モードを反転できます。

[UimPref](UimPref.md)で「SJ3 キー設定4」→「高度な設定」→「[SJ3](SJ3.md) かな/英数入力モードを反転」にキーを設定してください。

### vi協調モード ###

vi（クローン）でコマンドモードに戻る時、uimを直接入力モードに戻すことができます。

[UimPref](UimPref.md)で「SJ3 (高度)」→「特殊操作」→「vi協調モードを有効にする」のチェックボックスにチェックを入れてください。

標準のキー設定は以下のようになっています。

| 動作 | キー |
|:---|:---|
| vi協調モードでESCとして扱うキー | ESC、Ctrl+[ |

### ファイル ###

~/.uim.d/customs/custom-sj3.scm:: [UimPref](UimPref.md)の「SJ3」ファイル。~/.uim.d/customs/custom-sj3-advanced.scm:: [UimPref](UimPref.md)の「SJ3 (高度)」ファイル。~/.uim.d/customs/custom-sj3-keys(1,2,3,4).scm:: [UimPref](UimPref.md)の「SJ3 キー設定{1,2,3,4}」ファイル。

### 環境変数 ###

SJ3SERV

## カスタマイズ可能な項目 ##

### SJ3の変数 ###

| 動作 | 変数名 | 指定できる値 | 標準値 |
|:---|:----|:-------|:----|
| 文節区切りを表示 | sj3-show-segment-separator? | #t #f  | #f  |
| 文節区切り | sj3-segment-separator | "文字列"  | "|" |
| 候補ウィンドウを使用する | sj3-use-candidate-window? | #t #f  | #t  |
| 候補ウィンドウを表示するために変換キーを押す回数 | sj3-candidate-op-count | 数字     | 1   |
| 候補ウィンドウに一度に表示する候補数 | sj3-nr-candidate-max | 数字     | 10  |
| 数字キーで候補を選択する | sj3-select-candidate-by-numeral-key? | #t #f  | #f  |
| 標準の入力モード | default-widget\_sj3\_input\_mode | 'action\_sj3\_direct<br> 'action_sj3_hiragana<br> 'action_sj3_katakana<br> 'action_sj3_halfkana<br> 'action_sj3_halfwidth_alnum<br> 'action_sj3_fullwidth_alnum <table><thead><th> 'action_sj3_direct </th></thead><tbody>
<tr><td> 標準のかな入力方式 </td><td> default-widget_sj3_kana_input_method </td><td> 'action_sj3_roma<br> 'action_sj3_kana<br> 'action_sj3_azik </td><td> 'action_sj3_roma </td></tr>
<tr><td> ローカルマシン以外のSJ3サーバに接続する </td><td> sj3-use-remote-server? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> SJ3サーバ名 </td><td> sj3-server-name </td><td> "文字列"  </td><td> "localhost" </td></tr>
<tr><td> SJ3ユーザ名 </td><td> sj3-user-name </td><td> "文字列"  </td><td> (user-name) </td></tr>
<tr><td> vi協調モードを有効にする </td><td> sj3-use-with-vi? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> 直接入力モード(off状態)時も入力モード切り換えキーを有効にする </td><td> sj3-use-mode-transition-keys-in-off-mode? </td><td> #t #f  </td><td> #f  </td></tr></tbody></table>

<h4>SJ3の変数の依存関係</h4>

<ul><li>sj3-show-segment-separator? #f<br>
<ul><li>sj3-segment-separator</li></ul></li></ul>

<ul><li>sj3-use-candidate-window? #f<br>
<ul><li>sj3-candidate-op-count<br>
</li><li>sj3-nr-candidate-max<br>
</li><li>sj3-select-candidate-by-numeral-key?</li></ul></li></ul>

<ul><li>sj3-use-remote-server? #f<br>
<ul><li>sj3-server-name</li></ul></li></ul>

<h3>SJ3キー設定の変数</h3>

<table><thead><th> 動作 </th><th> キー変数名 </th></thead><tbody>
<tr><td> 次文節 </td><td> sj3-next-segment-key? </td></tr>
<tr><td> 前文節 </td><td> sj3-prev-segment-key? </td></tr>
<tr><td> 文節を伸ばす </td><td> sj3-extend-segment-key? </td></tr>
<tr><td> 文節を縮める </td><td> sj3-shrink-segment-key? </td></tr>
<tr><td> ひらがなに変換 </td><td> sj3-transpose-as-hiragana-key? </td></tr>
<tr><td> カタカナに変換 </td><td> sj3-transpose-as-katakana-key? </td></tr>
<tr><td> 半角カタカナに変換 </td><td> sj3-transpose-as-halfkana-key? </td></tr>
<tr><td> 半角英数字に変換 </td><td> sj3-transpose-as-halfwidth-alnum-key? </td></tr>
<tr><td> 全角英数字に変換 </td><td> sj3-transpose-as-fullwidth-alnum-key? </td></tr>
<tr><td> かな/カナ反転確定 </td><td> sj3-commit-as-opposite-kana-key? </td></tr>
<tr><td> オン </td><td> sj3-on-key? </td></tr>
<tr><td> オフ </td><td> sj3-off-key? </td></tr>
<tr><td> 変換開始 </td><td> sj3-begin-conv-key? </td></tr>
<tr><td> 確定 </td><td> sj3-commit-key </td></tr>
<tr><td> キャンセル </td><td> sj3-cancel-key? </td></tr>
<tr><td> 次候補 </td><td> sj3-next-candidate-key? </td></tr>
<tr><td> 前候補 </td><td> sj3-prev-candidate-key? </td></tr>
<tr><td> 候補ウィンドウの次ページ </td><td> sj3-next-page-key? </td></tr>
<tr><td> 候補ウィンドウの前ページ </td><td> sj3-prev-page-key? </td></tr>
<tr><td> 編集領域の先頭 </td><td> sj3-beginning-of-preedit-key? </td></tr>
<tr><td> 編集領域の末尾 </td><td> sj3-end-of-preedit-key? </td></tr>
<tr><td> カーソル以降を消去 </td><td> sj3-kill-key? </td></tr>
<tr><td> カーソル以前を消去 </td><td> sj3-kill-backward-key? </td></tr>
<tr><td> バックスペース </td><td> sj3-backspace-key? </td></tr>
<tr><td> デリート </td><td> sj3-delete-key? </td></tr>
<tr><td> 左に移動 </td><td> sj3-go-left-key? </td></tr>
<tr><td> 右に移動 </td><td> sj3-go-right-key? </td></tr>
<tr><td> vi協調モードでESCとして扱うキー </td><td> sj3-vi-escape-key? </td></tr>
<tr><td> ひらがな入力モード </td><td> sj3-hiragana-key? </td></tr>
<tr><td> カタカナ入力モード </td><td> sj3-katakana-key? </td></tr>
<tr><td> 半角カタカナ入力モード </td><td> sj3-halfkana-key? </td></tr>
<tr><td> 半角英数字入力モード </td><td> sj3-halfwidth-alnum-key? </td></tr>
<tr><td> 全角英数字入力モード </td><td> sj3-fullwidth-alnum-key? </td></tr>
<tr><td> ひらがな/カタカナ入力モードを反転 </td><td> sj3-kana-toggle-key? </td></tr>
<tr><td> かな/英数入力モードを反転 </td><td> sj3-alkana-toggle-key? </td></tr>