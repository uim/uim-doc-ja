= uim-ajax-ime =



## これは何？ ##

uimのAjax IMEモジュール。 かな漢字変換エンジン[Ajax IME](http://ajaxime.chasen.org/)や[ChaIME](http://cl.naist.jp/~mamoru-k/chaime/)で入力/変換などを行なう場合に使う。

'''このモジュールはリリース版には含まれていません。'''

## 使い方 ##

  1. あらかじめネットワークに接続しておいてください。
  1. [UimImSwitcher](UimImSwitcher.md)や[UimToolbar](UimToolbar.md)からAjax-IMEに切り換えてください。
    1. Ajax-IMEが見つからない場合は[UimPref](UimPref.md)を起動してください。
      * [UimToolbar](UimToolbar.md)の設定アイコンをクリック。
      * ターミナルエミュレータなどでuim-pref-gtk（もしくはuim-pref-qt）を実行。
    1. 起動したら、「全体設定」→「入力方式の利用準備」→「使用可能にする入力方式」の「編集...」ボタンを押して、左の有効アイテムにAjax-IMEを追加してください。
      * そこにもAjax-IMEが見つからない場合、uim-ajax-imeはインストールされていないのかもしれません。確認してみてください。
    1. 追加が完了したら、Ajax-IMEで入力したいアプリケーションを再起動してください。
  1. [UimImSwitcher](UimImSwitcher.md)や[UimToolbar](UimToolbar.md)による切り換えは一時的なものです。永続的な変更を望むなら[UimPref](UimPref.md)で設定する必要があります。
  1. [UimPref](UimPref.md)を起動したら、「全体設定」→「入力方式の利用準備」→「標準の入力方式を指定」のチェックボックスにチェックを入れます。
  1. そのすぐ下の「標準の入力方式」に、Ajax-IMEをセットしてください。

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
| カーソルを右へ移動 | →、Ctrl+f |
| カーソルを左へ移動 | ←、Ctrl+b |
| 編集領域の先頭へ移動 | Ctrl+a、Ctrl+← |
| 編集領域の末尾へ移動 | Ctrl+e、Ctrl+→ |
| カーソルより右の文字をすべて削除 | Ctrl+k |
| カーソルより左の文字をすべて削除 | Ctrl+u |
| カーソルの右の一字を削除 | Delete、Ctrl+d |
| カーソルの左の一字を削除 | BS、Ctrl+h |
| 変換開始 | Space |
| 次の変換候補へ移動 | Space、↓、Ctrl+n |
| 前の変換候補へ移動 | ↑、Ctrl+p |
| 次の変換候補ページへ移動 | PgDn |
| 前の変換候補ページへ移動 | PgUp |
| 変換確定 | Return、Ctrl+m、Ctrl+j |
| キャンセル | Esc、Ctrl+[、Ctrl+g |
| ひらがな/カタカナを反転変換し確定 | Q  |
| ひらがな変換 | F6 |
| カタカナ変換 | F7 |
| 半角カタカナ変換 | F8 |
| 全角英数字へ変換、大文字小文字を反転 | F9 |
| 半角英数字へ変換、大文字小文字を反転 | F10 |
| ひらがな、カタカナ、半角カタカナへの変換を循環 | 無変換 |

### 日本語と英語の交ぜ書き変換をする ###

入力中（編集領域が表示されている状態）で設定したキーを押すと、入力中の文字列を確定せず、ひらがな入力モードと半角英数入力モード、半角カタカナモードと全角英数モードを反転できます。

[UimPref](UimPref.md)で「Ajax-IME キー設定4」→「高度な設定」→「[Ajax-IME] かな/英数入力モードを反転」にキーを設定してください。

### vi協調モード ###

vi（クローン）でコマンドモードに戻る時、uimを直接入力モードに戻すことができます。

[UimPref](UimPref.md)で「Ajax-IME (高度)」→「特殊操作」→「vi協調モードを有効にする」のチェックボックスにチェックを入れてください。

標準のキー設定は以下のようになっています。

| 動作 | キー |
|:---|:---|
| vi協調モードでESCとして扱うキー | ESC、Ctrl+[ |

### ファイル ###

~/.uim.d/customs/custom-ajax-ime.scm:: [UimPref](UimPref.md)の「Ajax-IME」ファイル。~/.uim.d/customs/custom-ajax-ime-advanced.scm:: [UimPref](UimPref.md)の「Ajax-IME (高度)」ファイル。~/.uim.d/customs/custom-ajax-ime-keys{1,2,3,4}.scm:: [UimPref](UimPref.md)の「Ajax-IME キー設定{1,2,3,4}」ファイル。

## カスタマイズ可能な項目 ##

### Ajax-IMEの変数 ###

| 動作 | 変数名 | 指定できる値 | 標準値 |
|:---|:----|:-------|:----|
| 文節区切りを表示 | ajax-ime-show-segment-separator? | #t #f  | #f  |
| 文節区切り | ajax-ime-segment-separator | "文字列"  | "|" |
| 候補ウィンドウを使用する | ajax-ime-use-candidate-window? | #t #f  | #t  |
| 候補ウィンドウを表示するために変換キーを押す回数 | ajax-ime-candidate-op-count | 数字     | 1   |
| 候補ウィンドウに一度に表示する候補数 | ajax-ime-nr-candidate-max | 数字     | 10  |
| 数字キーで候補を選択する | ajax-ime-select-candidate-by-numeral-key? | #t #f  | #f  |
| 標準の入力モード | default-widget\_ajax-ime\_input\_mode | 'action\_ajax-ime\_direct<br> 'action_ajax-ime_hiragana<br> 'action_ajax-ime_katakana<br> 'action_ajax-ime_halfkana<br> 'action_ajax-ime_halfwidth_alnum<br> 'action_ajax-ime_fullwidth_alnum <table><thead><th> 'action_ajax-ime_direct </th></thead><tbody>
<tr><td> 標準のかな入力方式 </td><td> default-widget_ajax-ime_kana_input_method </td><td> 'action_ajax-ime_roma<br> 'action_ajax-ime_kana<br> 'action_ajax-ime_azik </td><td> 'action_ajax-ime_roma </td></tr>
<tr><td> Ajax IMEサーバを指定する </td><td> ajax-ime-url </td><td> 'ajax-ime<br> 'cha-ime </td><td> 'ajax-ime </td></tr>
<tr><td> vi協調モードを有効にする </td><td> ajax-ime-use-with-vi? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> 直接入力モード(off状態)時も入力モード切り換えキーを有効にする </td><td> ajax-ime-use-mode-transition-keys-in-off-mode? </td><td> #t #f  </td><td> #f  </td></tr></tbody></table>

<h4>Ajax-IMEの変数の依存関係</h4>

<ul><li>ajax-ime-show-segment-separator? #f<br>
<ul><li>ajax-ime-segment-separator</li></ul></li></ul>

<ul><li>ajax-ime-use-candidate-window? #f<br>
<ul><li>ajax-ime-candidate-op-count<br>
</li><li>ajax-ime-nr-candidate-max<br>
</li><li>ajax-ime-select-candidate-by-numeral-key?</li></ul></li></ul>

<h3>Ajax-IMEキー設定の変数</h3>

<table><thead><th> 動作 </th><th> キー変数名 </th></thead><tbody>
<tr><td> 次の文節 </td><td> ajax-ime-next-segment-key? </td></tr>
<tr><td> 前の文節 </td><td> ajax-ime-prev-segment-key? </td></tr>
<tr><td> 文節を伸ばす </td><td> ajax-ime-extend-segment-key? </td></tr>
<tr><td> 文節を縮める </td><td> ajax-ime-shrink-segment-key? </td></tr>
<tr><td> ひらがなに変換 </td><td> ajax-ime-transpose-as-hiragana-key? </td></tr>
<tr><td> カタカナに変換 </td><td> ajax-ime-transpose-as-katakana-key? </td></tr>
<tr><td> 半角カタカナに変換 </td><td> ajax-ime-transpose-as-halfkana-key? </td></tr>
<tr><td> 半角英数字に変換 </td><td> ajax-ime-transpose-as-halfwidth-alnum-key? </td></tr>
<tr><td> 全角英数字に変換 </td><td> ajax-ime-transpose-as-fullwidth-alnum-key? </td></tr>
<tr><td> かな/カナ反転確定 </td><td> ajax-ime-commit-as-opposite-kana-key? </td></tr>
<tr><td> オン </td><td> ajax-ime-on-key? </td></tr>
<tr><td> オフ </td><td> ajax-ime-off-key? </td></tr>
<tr><td> 変換開始 </td><td> ajax-ime-begin-conv-key? </td></tr>
<tr><td> 確定 </td><td> ajax-ime-commit-key? </td></tr>
<tr><td> キャンセル </td><td> ajax-ime-cancel-key? </td></tr>
<tr><td> 次候補 </td><td> ajax-ime-next-candidate-key? </td></tr>
<tr><td> 前候補 </td><td> ajax-ime-prev-candidate-key? </td></tr>
<tr><td> 候補ウィンドウの次ページ </td><td> ajax-ime-next-page-key? </td></tr>
<tr><td> 候補ウィンドウの前ページ </td><td> ajax-ime-prev-page-key? </td></tr>
<tr><td> 編集領域の先頭 </td><td> ajax-ime-beginning-of-preedit-key? </td></tr>
<tr><td> 編集領域の末尾 </td><td> ajax-ime-end-of-preedit-key? </td></tr>
<tr><td> カーソル以降を消去 </td><td> ajax-ime-kill-key? </td></tr>
<tr><td> カーソル以前を消去 </td><td> ajax-ime-kill-backward-key? </td></tr>
<tr><td> バックスペース </td><td> ajax-ime-backspace-key? </td></tr>
<tr><td> デリート </td><td> ajax-ime-delete-key? </td></tr>
<tr><td> 左に移動 </td><td> ajax-ime-go-left-key? </td></tr>
<tr><td> 右に移動 </td><td> ajax-ime-go-right-key? </td></tr>
<tr><td> vi協調モードでESCとして扱うキー </td><td> ajax-ime-vi-escape-key? </td></tr>
<tr><td> ひらがな入力モード </td><td> ajax-ime-hiragana-key? </td></tr>
<tr><td> カタカナ入力モード </td><td> ajax-ime-katakana-key? </td></tr>
<tr><td> 半角カタカナ入力モード </td><td> ajax-ime-halfkana-key? </td></tr>
<tr><td> 半角英数字入力モード </td><td> ajax-ime-halfwidth-alnum-key? </td></tr>
<tr><td> 全角英数字入力モード </td><td> ajax-ime-fullwidth-alnum-key? </td></tr>
<tr><td> ひらがな/カタカナ入力モードを反転 </td><td> ajax-ime-kana-toggle-key? </td></tr>
<tr><td> かな/英数入力モードを反転 </td><td> ajax-ime-alkana-toggle-key? </td></tr></tbody></table>

<h2>注意</h2>

学習機能と文節の伸縮機能はありません。