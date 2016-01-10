= uim-yahoo-jp =



## これは何？ ##

uimのYahoo! JAPAN かな漢字変換モジュール。 連文節かな漢字変換エンジン[Yahoo! JAPAN かな漢字変換Web API](http://developer.yahoo.co.jp/webapi/jlp/jim/v1/conversion.html)で入力/変換などを行なう場合に使う。

'''このモジュールはリリース版には含まれていません。''' また、このモジュールは標準では含まれません。 '''--with-expat'''をつけてuimをコンパイルする必要があります。

## 使い方 ##

  1. あらかじめ[Yahoo! JAPAN アプリケーションID](http://e.developer.yahoo.co.jp/webservices/register_application)を入手し、ネットワークに接続しておいてください。
  1. [UimPref](UimPref.md)を起動してください。
    * [UimToolbar](UimToolbar.md)の設定アイコンをクリック
    * ターミナルエミュレータなどでuim-pref-gtk（もしくはuim-pref-qt）を実行
  1. 起動したら、「Yahoo-Jp (高度)」→「Yahoo-Jp サーバ」→「Yahoo-Jpのapiキー」にアプリケーションIDを入力します。
  1. [UimImSwitcher](UimImSwitcher.md)や[UimToolbar](UimToolbar.md)からYahoo-Jpに切り換えてください。
    1. Yahoo-Jpが見つからない場合は[UimPref](UimPref.md)を起動してください。
    1. 起動したら、「全体設定」→「入力方式の利用準備」→「使用可能にする入力方式」の「編集...」ボタンを押して、左の有効アイテムにYahoo-Jpを追加してください。
      * そこにもYahoo-Jpが見つからない場合、uim-yahoo-jpはインストールされていないのかもしれません。確認してみてください。
    1. 追加が完了したら、Yahoo-Jpで入力したいアプリケーションを再起動してください。
  1. [UimImSwitcher](UimImSwitcher.md)や[UimToolbar](UimToolbar.md)による切り換えは一時的なものです。永続的な変更を望むなら[UimPref](UimPref.md)で設定する必要があります。
  1. [UimPref](UimPref.md)を起動したら、「全体設定」→「入力方式の利用準備」→「標準の入力方式を指定」のチェックボックスにチェックを入れます。
  1. そのすぐ下の「標準の入力方式」に、Yahoo-Jpをセットしてください。

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
| ひらがな/カタカナを反転変換し確定 | Q  |
| ひらがな変換 | F6 |
| カタカナ変換 | F7 |
| 半角カタカナ変換 | F8 |
| 全角英数字へ変換、大文字小文字を反転 | F9 |
| 半角英数字へ変換、大文字小文字を反転 | F10 |
| ひらがな、カタカナ、半角カタカナへの変換を循環 | 無変換 |
| 予測開始 | Tab、↓、Ctrl+n、Ctrl+i |
| 次の予測候補へ | Tab、↓、Ctrl+n、Ctrl+i |
| 前の予測候補へ | ↑、Ctrl+p |

### 日本語と英語の交ぜ書き変換をする ###

入力中（編集領域が表示されている状態）で設定したキーを押すと、入力中の文字列を確定せず、ひらがな入力モードと半角英数入力モード、半角カタカナモードと全角英数モードを反転できます。

[UimPref](UimPref.md)で「Yahoo-Jp キー設定4」→「高度な設定」→「[Yahoo-Jp] かな/英数入力モードを反転」にキーを設定してください。

### インクリメンタル予測入力をする ###

[UimPref](UimPref.md)で「Yahoo-Jp (高度)」→「予測入力」→「予測入力を有効にする」のチェックボックスにチェックを入れてください。

標準のキー設定は以下のようになっています。

| 動作 | キー |
|:---|:---|
| 次の予測候補へ | Tab、↓、Ctrl+n、Ctrl+i |
| 前の予測候補へ | ↑、Ctrl+p |

### vi協調モード ###

vi（クローン）でコマンドモードに戻る時、uimを直接入力モードに戻すことができます。

[UimPref](UimPref.md)で「Yahoo-Jp (高度)」→「特殊操作」→「vi協調モードを有効にする」のチェックボックスにチェックを入れてください。

標準のキー設定は以下のようになっています。

| 動作 | キー |
|:---|:---|
| vi協調モードでESCとして扱うキー | ESC、Ctrl+[ |

### ファイル ###

~/.uim.d/customs/custom-yahoo-jp.scm:: [UimPref](UimPref.md)の「Yahoo-Jp」ファイル。~/.uim.d/customs/custom-yahoo-jp-advanced.scm:: [UimPref](UimPref.md)の「Yahoo-Jp (高度)」ファイル。~/.uim.d/customs/custom-yahoo-jp-keys{1,2,3,4}.scm:: [UimPref](UimPref.md)の「Yahoo-Jp キー設定{1,2,3,4}」ファイル。

## カスタマイズ可能な項目 ##

### Yahoo-Jpの変数 ###

| 動作 | 変数名 | 指定できる値 | 標準値 |
|:---|:----|:-------|:----|
| 文節区切りを表示 | yahoo-jp-show-segment-separator? | #t #f  | #f  |
| 文節区切り | yahoo-jp-segment-separator | "文字列"  | "|" |
| 候補ウィンドウを使用する | yahoo-jp-use-candidate-window? | #t #f  | #t  |
| 候補ウィンドウを表示するために変換キーを押す回数 | yahoo-jp-candidate-op-count | 数字     | 1   |
| 候補ウィンドウに一度に表示する候補数 | yahoo-jp-nr-candidate-max | 数字     | 10  |
| 数字キーで候補を選択する | yahoo-jp-select-candidate-by-numeral-key? | #t #f  | #f  |
| 標準の入力モード | default-widget\_yahoo-jp\_input\_mode | 'action\_yahoo-jp\_direct<br> 'action_yahoo-jp_hiragana<br> 'action_yahoo-jp_katakana<br> 'action_yahoo-jp_halfkana<br> 'action_yahoo-jp_halfwidth_alnum<br> 'action_yahoo-jp_fullwidth_alnum <table><thead><th> 'action_yahoo-jp_direct </th></thead><tbody>
<tr><td> 標準のかな入力方式 </td><td> default-widget_yahoo-jp_kana_input_method </td><td> 'action_yahoo-jp_roma<br> 'action_yahoo-jp_kana<br> 'action_yahoo-jp_azik </td><td> 'action_yahoo-jp_roma </td></tr>
<tr><td> Yahoo-Jp server address </td><td> yahoo-jp-server </td><td> "文字列"  </td><td> "jlp.yahooapis.jp" </td></tr>
<tr><td> Yahoo-Jp service path </td><td> yahoo-jp-path </td><td> "文字列"  </td><td> "/JIMService/V1/" </td></tr>
<tr><td> Yahoo-Jpのapiキー </td><td> yahoo-jp-appid </td><td> "文字列"  </td><td> ""  </td></tr>
<tr><td> Use SSL </td><td> yahoo-jp-use-ssl? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> vi協調モードを有効にする </td><td> yahoo-jp-use-with-vi? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> 直接入力モード(off状態)時も入力モード切り換えキーを有効にする </td><td> yahoo-jp-use-mode-transition-keys-in-off-mode? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> 予測入力を有効にする </td><td> yahoo-jp-use-prediction? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> 数字キーで予測候補を選択する </td><td> yahoo-jp-select-prediction-by-numeral-key? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> 編集領域内に選んだ予測候補を表示する </td><td> yahoo-jp-use-implicit-commit-prediction? </td><td> #t #f  </td><td> #t  </td></tr>
<tr><td> Number of cache of prediction candidates </td><td> yahoo-jp-prediction-cache-words </td><td> 数字     </td><td> 256 </td></tr>
<tr><td> Character count to start input prediction </td><td> yahoo-jp-prediction-start-char-count </td><td> 数字     </td><td> 2   </td></tr></tbody></table>

<h4>Yahoo-Jpの変数の依存関係</h4>

<ul><li>yahoo-jp-show-segment-separator? #f<br>
<ul><li>yahoo-jp-segment-separator</li></ul></li></ul>

<ul><li>yahoo-jp-use-candidate-window? #f<br>
<ul><li>yahoo-jp-candidate-op-count<br>
</li><li>yahoo-jp-nr-candidate-max<br>
</li><li>yahoo-jp-select-candidate-by-numeral-key?<br>
</li><li>yahoo-jp-use-prediction?</li></ul></li></ul>

<ul><li>yahoo-jp-use-prediction? #f<br>
<ul><li>yahoo-jp-select-prediction-by-numeral-key?<br>
</li><li>yahoo-jp-use-implicit-commit-prediction?<br>
</li><li>yahoo-jp-prediction-cache-words<br>
</li><li>yahoo-jp-prediction-start-char-count</li></ul></li></ul>

<h3>Yahoo-Jpキー設定の変数</h3>

<table><thead><th> 動作 </th><th> キー変数名 </th></thead><tbody>
<tr><td> 次の文節 </td><td> yahoo-jp-next-segment-key? </td></tr>
<tr><td> 前の文節 </td><td> yahoo-jp-prev-segment-key? </td></tr>
<tr><td> 文節を伸ばす </td><td> yahoo-jp-extend-segment-key? </td></tr>
<tr><td> 文節を縮める </td><td> yahoo-jp-shrink-segment-key? </td></tr>
<tr><td> ひらがなに変換 </td><td> yahoo-jp-transpose-as-hiragana-key? </td></tr>
<tr><td> カタカナに変換 </td><td> yahoo-jp-transpose-as-katakana-key? </td></tr>
<tr><td> 半角カタカナに変換 </td><td> yahoo-jp-transpose-as-halfkana-key? </td></tr>
<tr><td> 半角英数字に変換 </td><td> yahoo-jp-transpose-as-halfwidth-alnum-key? </td></tr>
<tr><td> 全角英数字に変換 </td><td> yahoo-jp-transpose-as-fullwidth-alnum-key? </td></tr>
<tr><td> かな/カナ反転確定 </td><td> yahoo-jp-commit-as-opposite-kana-key? </td></tr>
<tr><td> オン </td><td> yahoo-jp-on-key? </td></tr>
<tr><td> オフ </td><td> yahoo-jp-off-key? </td></tr>
<tr><td> 変換開始 </td><td> yahoo-jp-begin-conv-key? </td></tr>
<tr><td> 確定 </td><td> yahoo-jp-commit-key? </td></tr>
<tr><td> キャンセル </td><td> yahoo-jp-cancel-key? </td></tr>
<tr><td> 次候補 </td><td> yahoo-jp-next-candidate-key? </td></tr>
<tr><td> 前候補 </td><td> yahoo-jp-prev-candidate-key? </td></tr>
<tr><td> 候補ウィンドウの次ページ </td><td> yahoo-jp-next-page-key? </td></tr>
<tr><td> 候補ウィンドウの前ページ </td><td> yahoo-jp-prev-page-key? </td></tr>
<tr><td> 編集領域の先頭 </td><td> yahoo-jp-beginning-of-preedit-key? </td></tr>
<tr><td> 編集領域の末尾 </td><td> yahoo-jp-end-of-preedit-key? </td></tr>
<tr><td> カーソル以降を消去 </td><td> yahoo-jp-kill-key? </td></tr>
<tr><td> カーソル以前を消去 </td><td> yahoo-jp-kill-backward-key? </td></tr>
<tr><td> バックスペース </td><td> yahoo-jp-backspace-key? </td></tr>
<tr><td> デリート </td><td> yahoo-jp-delete-key? </td></tr>
<tr><td> 左に移動 </td><td> yahoo-jp-go-left-key? </td></tr>
<tr><td> 右に移動 </td><td> yahoo-jp-go-right-key? </td></tr>
<tr><td> vi協調モードでESCとして扱うキー </td><td> yahoo-jp-vi-escape-key? </td></tr>
<tr><td> ひらがな入力モード </td><td> yahoo-jp-hiragana-key? </td></tr>
<tr><td> カタカナ入力モード </td><td> yahoo-jp-katakana-key? </td></tr>
<tr><td> 半角カタカナ入力モード </td><td> yahoo-jp-halfkana-key? </td></tr>
<tr><td> 半角英数字入力モード </td><td> yahoo-jp-halfwidth-alnum-key? </td></tr>
<tr><td> 全角英数字入力モード </td><td> yahoo-jp-fullwidth-alnum-key? </td></tr>
<tr><td> ひらがな/カタカナ入力モードを反転 </td><td> yahoo-jp-kana-toggle-key? </td></tr>
<tr><td> かな/英数入力モードを反転 </td><td> yahoo-jp-alkana-toggle-key? </td></tr>
<tr><td> Next prediction candidate </td><td> yahoo-jp-next-prediction-key? </td></tr>
<tr><td> Previous prediction candidate </td><td> yahoo-jp-prev-prediction-key? </td></tr>