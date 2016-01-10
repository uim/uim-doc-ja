= uim-wnn =



## これは何？ ##

uimのWnnモジュール。 クライアント・サーバ型のかな漢字変換システム[FreeWnn](http://freewnn.sourceforge.jp/)、[Wnn6](http://www.omronsoft.co.jp/SP/unix/wnn6/)、[Wnn7](http://www.omronsoft.co.jp/SP/pcunix/wnn7/)、[Wnn8](http://www.omronsoft.co.jp/SP/pcunix/wnn8/)で入力/変換などを行う場合に使う。

このモジュールは標準では含まれません。 '''--with-wnn'''をつけてuimをコンパイルする必要があります。

## 使い方 ##

  1. あらかじめWnnサーバを起動しておいてください。
  1. [UimImSwitcher](UimImSwitcher.md)や[UimToolbar](UimToolbar.md)からWnnに切り換えてください。
    1. Wnnが見つからない場合は[UimPref](UimPref.md)を起動してください。
      * [UimToolbar](UimToolbar.md)の設定アイコンをクリック
      * ターミナルエミュレータなどでuim-pref-gtk（もしくはuim-pref-qt）を実行
    1. 起動したら、「全体設定」→「入力方式の利用準備」→「使用可能にする入力方式」の「編集...」ボタンを押して、左の有効アイテムにWnnを追加してください。
      * そこにもWnnが見つからない場合、uim-wnnはインストールされていないのかもしれません。確認してみてください。
    1. 追加が完了したら、Wnnで入力したいアプリケーションを再起動してください。
  1. [UimImSwitcher](UimImSwitcher.md)や[UimToolbar](UimToolbar.md)による切り換えは一時的なものです。永続的な変更を望むなら[UimPref](UimPref.md)で設定する必要があります。
  1. [UimPref](UimPref.md)を起動したら、「全体設定」→「入力方式の利用準備」→「標準の入力方式を指定」のチェックボックスにチェックを入れます。
  1. そのすぐ下の「標準の入力方式」に、Wnnをセットしてください。

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

[UimPref](UimPref.md)で「Wnn キー設定4」→「高度な設定」→「[Wnn](Wnn.md) かな/英数入力モードを反転」にキーを設定してください。

### vi協調モード ###

vi（クローン）でコマンドモードに戻る時、uimを直接入力モードに戻すことができます。

[UimPref](UimPref.md)で「Wnn (高度)」→「特殊操作」→「vi協調モードを有効にする」のチェックボックスにチェックを入れてください。

標準のキー設定は以下のようになっています。

| 動作 | キー |
|:---|:---|
| vi協調モードでESCとして扱うキー | ESC、Ctrl+[ |

### ファイル ###

~/.uim.d/customs/custom-wnn.scm:: [UimPref](UimPref.md)の「Wnn」ファイル。~/.uim.d/customs/custom-wnn-advanced.scm:: [UimPref](UimPref.md)の「Wnn (高度)」ファイル。~/.uim.d/customs/custom-wnn-keys(1,2,3,4).scm:: [UimPref](UimPref.md)の「Wnn キー設定{1,2,3,4}」ファイル。

## カスタマイズ可能な項目 ##

### Wnnの変数 ###

| 動作 | 変数名 | 指定できる値 | 標準値 |
|:---|:----|:-------|:----|
| 文節区切りを表示 | wnn-show-segment-separator? | #t #f  | #f  |
| 文節区切り | wnn-segment-separator | "文字列"  | "|" |
| 候補ウィンドウを使用する | wnn-use-candidate-window? | #t #f  | #t  |
| 候補ウィンドウを表示するために変換キーを押す回数 | wnn-candidate-op-count | 数字     | 1   |
| 候補ウィンドウに一度に表示する候補数 | wnn-nr-candidate-max | 数字     | 10  |
| 数字キーで候補を選択する | wnn-select-candidate-by-numeral-key? | #t #f  | #f  |
| 標準の入力モード | default-widget\_wnn\_input\_mode | 'action\_wnn\_direct<br> 'action_wnn_hiragana<br> 'action_wnn_katakana<br> 'action_wnn_halfkana<br> 'action_wnn_halfwidth_alnum<br> 'action_wnn_fullwidth_alnum <table><thead><th> 'action_wnn_direct </th></thead><tbody>
<tr><td> 標準のかな入力方式 </td><td> default-widget_wnn_kana_input_method </td><td> 'action_wnn_roma<br> 'action_wnn_kana<br> 'action_wnn_azik </td><td> 'action_wnn_roma </td></tr>
<tr><td> ローカルマシン以外のWnnサーバに接続する </td><td> wnn-use-remote-server? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> Wnnサーバ名 </td><td> wnn-server-name </td><td> "文字列"  </td><td> "localhost" </td></tr>
<tr><td> Wnn設定ファイル </td><td> wnn-rcfile </td><td> "文字列"  </td><td> ""  </td></tr>
<tr><td> vi協調モードを有効にする </td><td> wnn-use-with-vi? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> 直接入力モード(off状態)時も入力モード切り換えキーを有効にする </td><td> wnn-use-mode-transition-keys-in-off-mode? </td><td> #t #f  </td><td> #f  </td></tr></tbody></table>

<h4>Wnnの変数の依存関係</h4>

<ul><li>wnn-show-segment-separator? #f<br>
<ul><li>wnn-segment-separator</li></ul></li></ul>

<ul><li>wnn-use-candidate-window? #f<br>
<ul><li>wnn-candidate-op-count<br>
</li><li>wnn-nr-candidate-max<br>
</li><li>wnn-select-candidate-by-numeral-key?</li></ul></li></ul>

<ul><li>wnn-use-remote-server? #f<br>
<ul><li>wnn-server-name</li></ul></li></ul>

<h3>Wnnキー設定の変数</h3>

<table><thead><th> 動作 </th><th> キー変数名 </th></thead><tbody>
<tr><td> 次文節 </td><td> wnn-next-segment-key? </td></tr>
<tr><td> 前文節 </td><td> wnn-prev-segment-key? </td></tr>
<tr><td> 文節を伸ばす </td><td> wnn-extend-segment-key? </td></tr>
<tr><td> 文節を縮める </td><td> wnn-shrink-segment-key? </td></tr>
<tr><td> ひらがなに変換 </td><td> wnn-transpose-as-hiragana-key? </td></tr>
<tr><td> カタカナに変換 </td><td> wnn-transpose-as-katakana-key? </td></tr>
<tr><td> 半角カタカナに変換 </td><td> wnn-transpose-as-halfkana-key? </td></tr>
<tr><td> 半角英数字に変換 </td><td> wnn-transpose-as-halfwidth-alnum-key? </td></tr>
<tr><td> 全角英数字に変換 </td><td> wnn-transpose-as-fullwidth-alnum-key? </td></tr>
<tr><td> かな/カナ反転確定 </td><td> wnn-commit-as-opposite-kana-key? </td></tr>
<tr><td> オン </td><td> wnn-on-key? </td></tr>
<tr><td> オフ </td><td> wnn-off-key? </td></tr>
<tr><td> 変換開始 </td><td> wnn-begin-conv-key? </td></tr>
<tr><td> 確定 </td><td> wnn-commit-key </td></tr>
<tr><td> キャンセル </td><td> wnn-cancel-key? </td></tr>
<tr><td> 次候補 </td><td> wnn-next-candidate-key? </td></tr>
<tr><td> 前候補 </td><td> wnn-prev-candidate-key? </td></tr>
<tr><td> 候補ウィンドウの次ページ </td><td> wnn-next-page-key? </td></tr>
<tr><td> 候補ウィンドウの前ページ </td><td> wnn-prev-page-key? </td></tr>
<tr><td> 編集領域の先頭 </td><td> wnn-beginning-of-preedit-key? </td></tr>
<tr><td> 編集領域の末尾 </td><td> wnn-end-of-preedit-key? </td></tr>
<tr><td> カーソル以降を消去 </td><td> wnn-kill-key? </td></tr>
<tr><td> カーソル以前を消去 </td><td> wnn-kill-backward-key? </td></tr>
<tr><td> バックスペース </td><td> wnn-backspace-key? </td></tr>
<tr><td> デリート </td><td> wnn-delete-key? </td></tr>
<tr><td> 左に移動 </td><td> wnn-go-left-key? </td></tr>
<tr><td> 右に移動 </td><td> wnn-go-right-key? </td></tr>
<tr><td> vi協調モードでESCとして扱うキー </td><td> wnn-vi-escape-key? </td></tr>
<tr><td> ひらがな入力モード </td><td> wnn-hiragana-key? </td></tr>
<tr><td> カタカナ入力モード </td><td> wnn-katakana-key? </td></tr>
<tr><td> 半角カタカナ入力モード </td><td> wnn-halfkana-key? </td></tr>
<tr><td> 半角英数入力モード </td><td> wnn-halfwidth-alnum-key? </td></tr>
<tr><td> 全角英数入力モード </td><td> wnn-fullwidth-alnum-key? </td></tr>
<tr><td> ひらがな/カタカナ入力モードを反転 </td><td> wnn-kana-toggle-key? </td></tr>
<tr><td> かな/英数入力モードを反転 </td><td> wnn-alkana-toggle-key? </td></tr>