= uim-canna =



## これは何？ ##

uimの[Canna](http://sourceforge.jp/projects/canna/)モジュール。 連文節かな漢字変換エンジンCannaで入力/変換などを行なう場合に使う。

このモジュールは標準では含まれません。 '''--with-canna'''をつけてuimをコンパイルする必要があります。

## 使い方 ##

  1. あらかじめCannaサーバを起動しておいてください。
  1. [UimImSwitcher](UimImSwitcher.md)や[UimToolbar](UimToolbar.md)からCannaに切り換えてください。
    1. Cannaが見つからない場合は[UimPref](UimPref.md)を起動してください。
      * [UimToolbar](UimToolbar.md)の設定アイコンをクリック
      * ターミナルエミュレータなどでuim-pref-gtk（もしくはuim-pref-qt）を実行
    1. 起動したら、「全体設定」→「入力方式の利用準備」→「使用可能にする入力方式」の「編集...」ボタンを押して、左の有効アイテムにCannaを追加してください。
      * そこにもCannaが見つからない場合、uim-cannaはインストールされていないのかもしれません。確認してみてください。
    1. 追加が完了したら、Cannaで入力したいアプリケーションを再起動してください。
  1. [UimImSwitcher](UimImSwitcher.md)や[UimToolbar](UimToolbar.md)による切り換えは一時的なものです。永続的な変更を望むなら[UimPref](UimPref.md)で設定する必要があります。
  1. [UimPref](UimPref.md)を起動したら、「全体設定」→「入力方式の利用準備」→「標準の入力方式を指定」のチェックボックスにチェックを入れます。
  1. そのすぐ下の「標準の入力方式」に、Cannaをセットしてください。

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
| オン/オフ | 全角/半角、Shift+Space、Ctrl+\ |
| ひらがな入力モードへ | Shift+F6 |
| カタカナ入力モードへ | Shift+F7 |
| 半角カタカナ入力モードへ | Shift+F8 |
| 全角英数入力モードへ | Shift+F9 |
| 半角英数入力モードへ | Shift+F10 |
| ひらがな/カタカナ入力モードを反転移行 | q  |
| 全角英数入力モードへ移行 | L  |
| 半角カタカナ入力モードへ移行 | Ctrl+q |
| カーソルを右へ移動 | →、Ctrl+f |
| カーソルを左へ移動 | ←、Ctrl+b |
| 編集領域の先頭へ移動 | Ctrl+a、Ctrl+← |
| 編集領域の末尾へ移動 | Ctrl+e、Ctrl+→ |
| カーソルより右の文字をすべて削除 | Ctrl+k |
| カーソルより左の文字をすべて削除 | Ctrl+u |
| カーソルの右の一字を削除 | Delete、Ctrl+d |
| カーソルの左の一字を削除 | BS、Ctrl+h |
| 変換開始 | Space |
| 文節を縮める | Shift+←、Ctrl+i |
| 文節を伸ばす | Shift+→、Ctrl+o |
| 次の変換候補へ移動 | Space、↓、Ctrl+n |
| 前の変換候補へ移動 | ↑、Ctrl+p |
| 次の変換候補ページへ移動 | PgDn |
| 前の変換候補ページへ移動 | PgUp |
| 次の文節へ移動 | →、Ctrl+f |
| 前の文節へ移動 | ←、Ctrl+b |
| 変換確定 | Return、Ctrl+m、Ctrl+j |
| キャンセル | Esc、Ctrl+[、Ctrl+g |
| ひらがな変換 | F6 |
| カタカナ変換 | F7 |
| 半角カタカナ変換 | F8 |
| 全角英数字へ変換、大文字小文字を反転 | F9 |
| 半角英数字へ変換、大文字小文字を反転 | F10 |
| ひらがな、カタカナ、半角カタカナへの変換を循環 | 無変換 |

### 日本語と英語の交ぜ書き変換をする ###

入力中（編集領域が表示されている状態）で設定したキーを押すと、入力中の文字列を確定せず、ひらがな入力モードと半角英数入力モード、半角カタカナモードと全角英数モードを反転できます。

[UimPref](UimPref.md)で「Canna キー設定4」→「高度な設定」→「[Canna](Canna.md) かな/英数入力モードを反転」にキーを設定してください。

### vi協調モード ###

vi（クローン）でコマンドモードに戻る時、uimを直接入力モードに戻すことができます。

[UimPref](UimPref.md)で「Canna (高度)」→「特殊操作」→「vi協調モードを有効にする」のチェックボックスにチェックを入れてください。

標準のキー設定は以下のようになっています。

| 動作 | キー |
|:---|:---|
| vi協調モードでESCとして扱うキー | ESC、Ctrl+[ |

### Canna互換プロトコル ###

uim-cannaでCanna互換プロトコルを採用している、幾つかの変換エンジンも利用できるようです。

  * [なつめ](http://natume.sourceforge.jp/)
  * [Whiz](http://yui.mine.nu/whiz/whiz.html)
  * [wime](http://www.venus.sannet.ne.jp/thomas/wime/)

### ファイル ###

~/.uim.d/customs/custom-canna.scm:: [UimPref](UimPref.md)の「Canna」ファイル。~/.uim.d/customs/custom-cannaserver.scm:: [UimPref](UimPref.md)の「Canna サーバ」ファイル。~/.uim.d/customs/custom-canna-advanced.scm:: [UimPref](UimPref.md)の「Canna (高度)」ファイル。~/.uim.d/customs/custom-canna-keys{1,2,3,4}.scm:: [UimPref](UimPref.md)の「Canna キー設定{1,2,3,4}」ファイル。

## カスタマイズ可能な項目 ##

### Cannaの変数 ###

| 動作 | 変数名 | 指定できる値 | 標準値 |
|:---|:----|:-------|:----|
| 文節区切りを表示 | canna-show-segment-separator? | #t #f  | #f  |
| 文節区切り | canna-segment-separator | "文字列"  | "|" |
| 候補ウィンドウを使用する | canna-use-candidate-window? | #t #f  | #t  |
| 候補ウィンドウを表示するために変換キーを押す回数 | canna-candidate-op-count | 数字     | 1   |
| 候補ウィンドウに一度に表示する候補数 | canna-nr-candidate-max | 数字     | 10  |
| 数字キーで候補を選択する | canna-select-candidate-by-numeral-key? | #t #f  | #f  |
| 標準の入力モード | default-widget\_canna\_input\_mode | 'action\_canna\_direct<br> 'action_canna_hiragana<br> 'action_canna_katakana<br> 'action_canna_halfkana<br> 'action_canna_halfwidth_alnum<br> 'action_canna_fullwidth_alnum <table><thead><th> 'action_canna_direct </th></thead><tbody>
<tr><td> 標準のかな入力方式 </td><td> default-widget_canna_kana_input_method </td><td> 'action_canna_roma<br> 'action_canna_kana<br> 'action_canna_azik </td><td> 'action_canna_roma </td></tr>
<tr><td> Cannaサーバを指定する </td><td> custom-activate-canna-server-name? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> Cannaサーバ名 </td><td> custom-preserved-canna-server-name </td><td> "文字列"  </td><td> ""  </td></tr>
<tr><td> vi協調モードを有効にする </td><td> canna-use-with-vi? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> 直接入力モード(off状態)時も入力モード切り換えキーを有効にする </td><td> canna-use-mode-transition-keys-in-off-mode? </td><td> #t #f  </td><td> #f  </td></tr></tbody></table>

<h4>Cannaの変数の依存関係</h4>

<ul><li>canna-show-segment-separator? #f<br>
<ul><li>canna-segment-separator</li></ul></li></ul>

<ul><li>canna-use-candidate-window? #f<br>
<ul><li>canna-candidate-op-count<br>
</li><li>canna-nr-candidate-max<br>
</li><li>canna-select-candidate-by-numeral-key?</li></ul></li></ul>

<ul><li>custom-activate-canna-server-name? #f<br>
<ul><li>custom-preserved-canna-server-name</li></ul></li></ul>

<h3>Cannaキー設定の変数</h3>

<table><thead><th> 動作 </th><th> キー変数名 </th></thead><tbody>
<tr><td> 次の文節 </td><td> canna-next-segment-key? </td></tr>
<tr><td> 前の文節 </td><td> canna-prev-segment-key? </td></tr>
<tr><td> 文節を伸ばす </td><td> canna-extend-segment-key? </td></tr>
<tr><td> 文節を縮める </td><td> canna-shrink-segment-key? </td></tr>
<tr><td> ひらがなに変換 </td><td> canna-transpose-as-hiragana-key? </td></tr>
<tr><td> カタカナに変換 </td><td> canna-transpose-as-katakana-key? </td></tr>
<tr><td> 半角カタカナに変換 </td><td> canna-transpose-as-halfkana-key? </td></tr>
<tr><td> 半角英数字に変換 </td><td> canna-transpose-as-halfwidth-alnum-key? </td></tr>
<tr><td> 全角英数字に変換 </td><td> canna-transpose-as-fullwidth-alnum-key? </td></tr>
<tr><td> かな/カナ反転確定 </td><td> canna-commit-as-opposite-kana-key? </td></tr>
<tr><td> オン </td><td> canna-on-key? </td></tr>
<tr><td> オフ </td><td> canna-off-key? </td></tr>
<tr><td> 変換開始 </td><td> canna-begin-conv-key? </td></tr>
<tr><td> 確定 </td><td> canna-commit-key? </td></tr>
<tr><td> キャンセル </td><td> canna-cancel-key? </td></tr>
<tr><td> 次候補 </td><td> canna-next-candidate-key? </td></tr>
<tr><td> 前候補 </td><td> canna-prev-candidate-key? </td></tr>
<tr><td> 候補ウィンドウの次ページ </td><td> canna-next-page-key? </td></tr>
<tr><td> 候補ウィンドウの前ページ </td><td> canna-prev-page-key? </td></tr>
<tr><td> 編集領域の先頭 </td><td> canna-beginning-of-preedit-key? </td></tr>
<tr><td> 編集領域の末尾 </td><td> canna-end-of-preedit-key? </td></tr>
<tr><td> カーソル以降を消去 </td><td> canna-kill-key? </td></tr>
<tr><td> カーソル以前を消去 </td><td> canna-kill-backward-key? </td></tr>
<tr><td> バックスペース </td><td> canna-backspace-key? </td></tr>
<tr><td> デリート </td><td> canna-delete-key? </td></tr>
<tr><td> 左に移動 </td><td> canna-go-left-key? </td></tr>
<tr><td> 右に移動 </td><td> canna-go-right-key? </td></tr>
<tr><td> vi協調モードでESCとして扱うキー </td><td> canna-vi-escape-key? </td></tr>
<tr><td> ひらがな入力モード </td><td> canna-hiragana-key? </td></tr>
<tr><td> カタカナ入力モード </td><td> canna-katakana-key? </td></tr>
<tr><td> 半角カタカナ入力モード </td><td> canna-halfkana-key? </td></tr>
<tr><td> 半角英数入力モード </td><td> canna-halfwidth-alnum-key? </td></tr>
<tr><td> 全角英数入力モード </td><td> canna-fullwidth-alnum-key? </td></tr>
<tr><td> ひらがな/カタカナ入力モードを反転 </td><td> canna-kana-toggle-key? </td></tr>
<tr><td> かな/英数入力モードを反転 </td><td> canna-alkana-toggle-key? </td></tr></tbody></table>

<h2>仕様</h2>

~/.cannaファイルは読みません。 読ませるにはuim-cannaを書き直す必要があるようです。<br>
<br>
<a href='http://lists.sourceforge.jp/mailman/archives/canna-dev/2005-September/000348.html'>http://lists.sourceforge.jp/mailman/archives/canna-dev/2005-September/000348.html</a>