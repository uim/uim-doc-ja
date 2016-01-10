= uim-anthy =



## これは何？ ##

uimのhttp://anthy.sourceforge.jp/|Anthyモジュール。 連文節かな漢字変換エンジンAnthyで入力/変換などを行なう場合に使う。

uim-anthyのUTF-8版は標準では含まれません。 UTF-8に対応したAnthy（8622以降）をインストールし、'''--with-anthy-utf8'''をつけてuimをコンパイルする必要があります。

## 使い方 ##

  1. [UimImSwitcher](UimImSwitcher.md)や[UimToolbar](UimToolbar.md)からAnthyに切り換えてください。
    1. Anthyが見つからない場合は[UimPref](UimPref.md)を起動してください。
      * [UimToolbar](UimToolbar.md)の設定アイコンをクリック
      * ターミナルエミュレータなどでuim-pref-gtk（もしくはuim-pref-qt）を実行
    1. 起動したら、「全体設定」→「入力方式の利用準備」→「使用可能にする入力方式」の「編集...」ボタンを押して、左の有効アイテムにAnthyを追加してください。
      * そこにもAnthyが見つからない場合、uim-anthyはインストールされていないのかもしれません。確認してみてください。
    1. 追加が完了したら、Anthyで入力したいアプリケーションを再起動してください。
  1. [UimImSwitcher](UimImSwitcher.md)や[UimToolbar](UimToolbar.md)による切り換えは一時的なものです。永続的な変更を望むなら[UimPref](UimPref.md)で設定する必要があります。
  1. [UimPref](UimPref.md)を起動したら、「全体設定」→「入力方式の利用準備」→「標準の入力方式を指定」のチェックボックスにチェックを入れます。
  1. そのすぐ下の「標準の入力方式」に、Anthyをセットしてください。

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

[UimPref](UimPref.md)で「Anthy キー設定4」→「高度な設定」→「[Anthy](Anthy.md) かな/英数入力モードを反転」にキーを設定してください。

### 予測入力をする ###

[UimPref](UimPref.md)で「Anthy (高度)」→「予測入力」→「予測入力を有効にする」のチェックボックスにチェックを入れてください。

標準のキー設定は以下のようになっています。

| 動作 | キー |
|:---|:---|
| 次の予測候補へ | Tab、↓、Ctrl+n、Ctrl+i |
| 前の予測候補へ | ↑、Ctrl+p |

### vi協調モード ###

vi（クローン）でコマンドモードに戻る時、uimを直接入力モードに戻すことができます。

[UimPref](UimPref.md)で「Anthy (高度)」→「特殊操作」→「vi協調モードを有効にする」のチェックボックスにチェックを入れてください。

標準のキー設定は以下のようになっています。

| 動作 | キー |
|:---|:---|
| vi協調モードでESCとして扱うキー | ESC、Ctrl+[ |

### ファイル ###

~/.uim.d/customs/custom-anthy.scm:: [UimPref](UimPref.md)の「Antny」ファイル。~/.uim.d/customs/custom-anthy-advanced.scm:: [UimPref](UimPref.md)の「Anthy (高度)」ファイル。~/.uim.d/customs/custom-anthy-keys{1,2,3,4}.scm:: [UimPref](UimPref.md)の「Anthy キー設定{1,2,3,4}」ファイル。~/.uim.d/customs/custom-anthy-utf8.scm:: [UimPref](UimPref.md)の「Anthy (UTF-8)」ファイル。

### 環境変数 ###

ANTHY\_HISTORY\_FILE:: 絶対パスでファイル名を指定すると、そのファイルに変換履歴が保存される。ANTHY\_ENABLE\_DEBUG\_PRINT:: デバッグプリントを有効にする。ANTHY\_DISABLE\_DEBUG\_PRINTが指定されていると無視されます。ANTHY\_SPLITTER\_PRINT:: デバッグプリントの構造体を指定する。'''w'''はwordlist、'''m'''はmetaword、'''l'''はlatticeのnode、'''i'''は自立語のマッチした品詞、'''c'''は?を表示。ANTHY\_DISABLE\_DEBUG\_PRINT:: デバッグプリントを無効にする。

## カスタマイズ可能な項目 ##

### Anthyの変数 ###

| 動作 | 変数名 | 指定できる値 | 標準値 |
|:---|:----|:-------|:----|
| 文節区切りを表示 | anthy-show-segment-separator? | #t #f  | #f  |
| 文節区切り | anthy-segment-separator | "文字列"  | "|" |
| 候補ウィンドウを使用する | anthy-use-candidate-window? | #t #f  | #t  |
| 候補ウィンドウを表示するために変換キーを押す回数 | anthy-candidate-op-count | 数字     | 1   |
| 候補ウィンドウに一度に表示する候補数 | anthy-nr-candidate-max | 数字     | 10  |
| 数字キーで候補を選択する | anthy-select-candidate-by-numeral-key? | #t #f  | #f  |
| 標準の入力モード | default-widget\_anthy\_input\_mode | 'action\_anthy\_direct<br> 'action_anthy_hiragana<br> 'action_anthy_katakana<br> 'action_anthy_halfkana<br> 'action_anthy_halfwidth_alnum<br> 'action_anthy_fullwidth_alnum <table><thead><th> 'action_anthy_direct </th></thead><tbody>
<tr><td> 標準のかな入力方式 </td><td> default-widget_anthy_kana_input_method </td><td> 'action_anthy_roma<br> 'action_anthy_kana<br> 'action_anthy_azik </td><td> 'action_anthy_roma </td></tr>
<tr><td> 予測入力を有効にする </td><td> anthy-use-prediction? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> 数字キーで予測候補を選択する </td><td> anthy-select-prediction-by-numeral-key? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> 編集領域内に選んだ予測候補を表示する </td><td> anthy-use-implicit-commit-prediction? </td><td> #t #f  </td><td> #t  </td></tr>
<tr><td> vi協調モードを有効にする </td><td> anthy-use-with-vi? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> 直接入力モード(off状態)時も入力モード切り換えキーを有効にする </td><td> anthy-use-mode-transition-keys-in-off-mode? </td><td> #t #f  </td><td> #f  </td></tr></tbody></table>

<h4>Anthyの変数の依存関係</h4>

<ul><li>anthy-show-segment-separator? #f<br>
<ul><li>anthy-segment-separator</li></ul></li></ul>

<ul><li>anthy-use-candidate-window? #f<br>
<ul><li>anthy-candidate-op-count<br>
</li><li>anthy-nr-candidate-max<br>
</li><li>anthy-select-candidate-by-numeral-key?</li></ul></li></ul>

<ul><li>anthy-use-prediction? #f<br>
<ul><li>anthy-select-prediction-by-numeral-key?<br>
</li><li>anthy-use-implicit-commit-prediction?</li></ul></li></ul>

<h3>Anthy (UTF-8)の変数</h3>

<table><thead><th> 動作 </th><th> 変数名 </th><th> 指定できる値 </th><th> 標準値 </th></thead><tbody>
<tr><td> 標準の入力モード </td><td> default-widget_anthy_utf8_input_mode </td><td> 'action_anthy_utf8_direct<br> 'action_anthy_utf8_hiragana<br> 'action_anthy_utf8_katakana<br> 'action_anthy_utf8_halfkana<br> 'action_anthy_utf8_halfwidth_alnum<br> 'action_anthy_utf8_fullwidth_alnum </td><td> 'action_anthy_utf8_direct </td></tr>
<tr><td> 標準のかな入力方式 </td><td> default-widget_anthy_utf8_kana_input_method </td><td> 'action_anthy_utf8_roma<br> 'action_anthy_utf8_kana<br> 'action_anthy_utf8_azik </td><td> 'action_anthy_utf8_roma </td></tr></tbody></table>

<h3>Anthyキー設定の変数</h3>

<table><thead><th> 動作 </th><th> キー変数名 </th></thead><tbody>
<tr><td> 次文節 </td><td> anthy-next-segment-key? </td></tr>
<tr><td> 前文節 </td><td> anthy-prev-segment-key? </td></tr>
<tr><td> 文節を伸ばす </td><td> anthy-extend-segment-key? </td></tr>
<tr><td> 文節を縮める </td><td> anthy-shrink-segment-key? </td></tr>
<tr><td> ひらがなに変換 </td><td> anthy-transpose-as-hiragana-key? </td></tr>
<tr><td> カタカナに変換 </td><td> anthy-transpose-as-katakana-key? </td></tr>
<tr><td> 半角カタカナに変換 </td><td> anthy-transpose-as-halfkana-key? </td></tr>
<tr><td> 半角英数字に変換 </td><td> anthy-transpose-as-halfwidth-alnum-key? </td></tr>
<tr><td> 全角英数字に変換 </td><td> anthy-transpose-as-fullwidth-alnum-key? </td></tr>
<tr><td> かな/カナ反転確定 </td><td> anthy-commit-as-opposite-kana-key? </td></tr>
<tr><td> オン </td><td> anthy-on-key? </td></tr>
<tr><td> オフ </td><td> anthy-off-key? </td></tr>
<tr><td> 変換開始 </td><td> anthy-begin-conv-key? </td></tr>
<tr><td> 確定 </td><td> anthy-commit-key </td></tr>
<tr><td> キャンセル </td><td> anthy-cancel-key? </td></tr>
<tr><td> 次候補 </td><td> anthy-next-candidate-key? </td></tr>
<tr><td> 前候補 </td><td> anthy-prev-candidate-key? </td></tr>
<tr><td> 候補ウィンドウの次ページ </td><td> anthy-next-page-key? </td></tr>
<tr><td> 候補ウィンドウの前ページ </td><td> anthy-prev-page-key? </td></tr>
<tr><td> 編集領域の先頭 </td><td> anthy-beginning-of-preedit-key? </td></tr>
<tr><td> 編集領域の末尾 </td><td> anthy-end-of-preedit-key? </td></tr>
<tr><td> カーソル以降を消去 </td><td> anthy-kill-key? </td></tr>
<tr><td> カーソル以前を消去 </td><td> anthy-kill-backward-key? </td></tr>
<tr><td> バックスペース </td><td> anthy-backspace-key? </td></tr>
<tr><td> デリート </td><td> anthy-delete-key? </td></tr>
<tr><td> 左に移動 </td><td> anthy-go-left-key? </td></tr>
<tr><td> 右に移動 </td><td> anthy-go-right-key? </td></tr>
<tr><td> vi協調モードでESCとして扱うキー </td><td> anthy-vi-escape-key? </td></tr>
<tr><td> ひらがな入力モード </td><td> anthy-hiragana-key? </td></tr>
<tr><td> カタカナ入力モード </td><td> anthy-katakana-key? </td></tr>
<tr><td> 半角カタカナ入力モード </td><td> anthy-halfkana-key? </td></tr>
<tr><td> 半角英数入力モード </td><td> anthy-halfwidth-alnum-key? </td></tr>
<tr><td> 全角英数入力モード </td><td> anthy-fullwidth-alnum-key? </td></tr>
<tr><td> ひらがな/カタカナ入力モードを反転 </td><td> anthy-kana-toggle-key? </td></tr>
<tr><td> かな/英数入力モードを反転 </td><td> anthy-alkana-toggle-key? </td></tr>
<tr><td> 次予測候補 </td><td> anthy-next-prediction-key? </td></tr>
<tr><td> 前予測候補 </td><td> anthy-prev-prediction-key? </td></tr>