= uim-social-ime =



## これは何？ ##

uimの[Social IME](http://www.social-ime.com/)モジュール。 連文節かな漢字変換エンジンSocial IMEの[Web API](http://www.social-ime.com/api.html)で入力/変換などを行なう場合に使う。

'''このモジュールはリリース版には含まれていません。'''

## 使い方 ##

  1. あらかじめネットワークに接続しておいてください。
  1. [UimImSwitcher](UimImSwitcher.md)や[UimToolbar|UimToolbar]からSocial-IMEに切り換えてください。
    1. Social-IMEが見つからない場合は[UimPref](UimPref.md)を起動してください。
      * [UimToolbar](UimToolbar.md)の設定アイコンをクリック。
      * ターミナルエミュレータなどでuim-pref-gtk（もしくはuim-pref-qt）を実行。
    1. 起動したら、「全体設定」→「入力方式の利用準備」→「使用可能にする入力方式」の「編集...」ボタンを押して、左の有効アイテムにSocial-IMEを追加してください。
      * そこにもSocial-IMEが見つからない場合、uim-social-imeはインストールされていないのかもしれません。確認してみてください。
    1. 追加が完了したら、Social-IMEで入力したいアプリケーションを再起動してください。
  1. [UimImSwitcher](UimImSwitcher.md)や[UimToolbar|UimToolbar]による切り換えは一時的なものです。永続的な変更を望むなら[UimPref|UimPref]で設定する必要があります。
  1. [UimPref](UimPref.md)を起動したら、「全体設定」→「入力方式の利用準備」→「標準の入力方式を指定」のチェックボックスにチェックを入れます。
  1. そのすぐ下の「標準の入力方式」に、Social-IMEをセットしてください。

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

[UimPref](UimPref.md)で「Social-IME キー設定4」→「高度な設定」→「[Social-IME] かな/英数入力モードを反転」にキーを設定してください。

### インクリメンタル予測入力をする ###

[UimPref](UimPref.md)で「Social-IME (高度)」→「予測入力」→「予測入力を有効にする」のチェックボックスにチェックを入れてください。

標準のキー設定は以下のようになっています。

| 動作 | キー |
|:---|:---|
| 次の予測候補へ | Tab、↓、Ctrl+n、Ctrl+i |
| 前の予測候補へ | ↑、Ctrl+p |

### vi協調モード ###

vi（クローン）でコマンドモードに戻る時、uimを直接入力モードに戻すことができます。

[UimPref](UimPref.md)で「Social-IME (高度)」→「特殊操作」→「vi協調モードを有効にする」のチェックボックスにチェックを入れてください。

標準のキー設定は以下のようになっています。

| 動作 | キー |
|:---|:---|
| vi協調モードでESCとして扱うキー | ESC、Ctrl+[ |

### ファイル ###

~/.uim.d/customs/custom-social-ime.scm:: [UimPref](UimPref.md)の「Social-IME」ファイル。~/.uim.d/customs/custom-social-ime-advanced.scm:: [UimPref](UimPref.md)の「Social-IME (高度)」ファイル。~/.uim.d/customs/custom-social-ime-keys{1,2,3,4}.scm:: [UimPref](UimPref.md)の「Social-IME キー設定{1,2,3,4}」ファイル。

## カスタマイズ可能な項目 ##

### Social-IMEの変数 ###

| 動作 | 変数名 | 指定できる値 | 標準値 |
|:---|:----|:-------|:----|
| 文節区切りを表示 | social-ime-show-segment-separator? | #t #f  | #f  |
| 文節区切り | social-ime-segment-separator | "文字列"  | "|" |
| 候補ウィンドウを使用する | social-ime-use-candidate-window? | #t #f  | #t  |
| 候補ウィンドウを表示するために変換キーを押す回数 | social-ime-candidate-op-count | 数字     | 1   |
| 候補ウィンドウに一度に表示する候補数 | social-ime-nr-candidate-max | 数字     | 10  |
| 数字キーで候補を選択する | social-ime-select-candidate-by-numeral-key? | #t #f  | #f  |
| 標準の入力モード | default-widget\_social-ime\_input\_mode | 'action\_social-ime\_direct<br> 'action_social-ime_hiragana<br> 'action_social-ime_katakana<br> 'action_social-ime_halfkana<br> 'action_social-ime_halfwidth_alnum<br> 'action_social-ime_fullwidth_alnum <table><thead><th> 'action_social-ime_direct </th></thead><tbody>
<tr><td> 標準のかな入力方式 </td><td> default-widget_social-ime_kana_input_method </td><td> 'action_social-ime_roma<br> 'action_social-ime_kana<br> 'action_social-ime_azik </td><td> 'action_social-ime_roma </td></tr>
<tr><td> Social-IME server address </td><td> social-ime-server </td><td> "文字列"  </td><td> "www.social-ime.com" </td></tr>
<tr><td> Social-IME server path </td><td> social-ime-path </td><td> "文字列"  </td><td> "/api/" </td></tr>
<tr><td> Social-IME server prediction API path </td><td> social-ime-prediction-api-path </td><td> "文字列"  </td><td> "/api2/predict.php" </td></tr>
<tr><td> Social-IMEユーザ名 </td><td> social-ime-user </td><td> "文字列"  </td><td> "user-name" </td></tr>
<tr><td> vi協調モードを有効にする </td><td> social-ime-use-with-vi? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> 直接入力モード(off状態)時も入力モード切り換えキーを有効にする </td><td> social-ime-use-mode-transition-keys-in-off-mode? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> 予測入力を有効にする </td><td> social-ime-use-prediction? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> 数字キーで予測候補を選択する </td><td> social-ime-select-prediction-by-numeral-key? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> 編集領域内に選んだ予測候補を表示する </td><td> social-ime-use-implicit-commit-prediction? </td><td> #t #f  </td><td> #t  </td></tr>
<tr><td> Number of cache of prediction candidates </td><td> social-ime-prediction-cache-words </td><td> 数字     </td><td> 256 </td></tr>
<tr><td> Character count to start input prediction </td><td> social-ime-prediction-start-char-count </td><td> 数字     </td><td> 2   </td></tr></tbody></table>

<h4>Social-IMEの変数の依存関係</h4>

<ul><li>social-ime-show-segment-separator? #f<br>
<ul><li>social-ime-segment-separator</li></ul></li></ul>

<ul><li>social-ime-use-candidate-window? #f<br>
<ul><li>social-ime-candidate-op-count<br>
</li><li>social-ime-nr-candidate-max<br>
</li><li>social-ime-select-candidate-by-numeral-key?<br>
</li><li>social-ime-use-prediction?</li></ul></li></ul>

<ul><li>social-ime-use-prediction? #f<br>
<ul><li>social-ime-select-prediction-by-numeral-key?<br>
</li><li>social-ime-use-implicit-commit-prediction?<br>
</li><li>social-ime-prediction-cache-words<br>
</li><li>social-ime-prediction-start-char-count</li></ul></li></ul>

<h3>Social-IMEキー設定の変数</h3>

<table><thead><th> 動作 </th><th> キー変数名 </th></thead><tbody>
<tr><td> 次の文節 </td><td> social-ime-next-segment-key? </td></tr>
<tr><td> 前の文節 </td><td> social-ime-prev-segment-key? </td></tr>
<tr><td> 文節を伸ばす </td><td> social-ime-extend-segment-key? </td></tr>
<tr><td> 文節を縮める </td><td> social-ime-shrink-segment-key? </td></tr>
<tr><td> ひらがなに変換 </td><td> social-ime-transpose-as-hiragana-key? </td></tr>
<tr><td> カタカナに変換 </td><td> social-ime-transpose-as-katakana-key? </td></tr>
<tr><td> 半角カタカナに変換 </td><td> social-ime-transpose-as-halfkana-key? </td></tr>
<tr><td> 半角英数字に変換 </td><td> social-ime-transpose-as-halfwidth-alnum-key? </td></tr>
<tr><td> 全角英数字に変換 </td><td> social-ime-transpose-as-fullwidth-alnum-key? </td></tr>
<tr><td> かな/カナ反転確定 </td><td> social-ime-commit-as-opposite-kana-key? </td></tr>
<tr><td> オン </td><td> social-ime-on-key? </td></tr>
<tr><td> オフ </td><td> social-ime-off-key? </td></tr>
<tr><td> 変換開始 </td><td> social-ime-begin-conv-key? </td></tr>
<tr><td> 確定 </td><td> social-ime-commit-key? </td></tr>
<tr><td> キャンセル </td><td> social-ime-cancel-key? </td></tr>
<tr><td> 次候補 </td><td> social-ime-next-candidate-key? </td></tr>
<tr><td> 前候補 </td><td> social-ime-prev-candidate-key? </td></tr>
<tr><td> 候補ウィンドウの次ページ </td><td> social-ime-next-page-key? </td></tr>
<tr><td> 候補ウィンドウの前ページ </td><td> social-ime-prev-page-key? </td></tr>
<tr><td> 編集領域の先頭 </td><td> social-ime-beginning-of-preedit-key? </td></tr>
<tr><td> 編集領域の末尾 </td><td> social-ime-end-of-preedit-key? </td></tr>
<tr><td> カーソル以降を消去 </td><td> social-ime-kill-key? </td></tr>
<tr><td> カーソル以前を消去 </td><td> social-ime-kill-backward-key? </td></tr>
<tr><td> バックスペース </td><td> social-ime-backspace-key? </td></tr>
<tr><td> デリート </td><td> social-ime-delete-key? </td></tr>
<tr><td> 左に移動 </td><td> social-ime-go-left-key? </td></tr>
<tr><td> 右に移動 </td><td> social-ime-go-right-key? </td></tr>
<tr><td> vi協調モードでESCとして扱うキー </td><td> social-ime-vi-escape-key? </td></tr>
<tr><td> ひらがな入力モード </td><td> social-ime-hiragana-key? </td></tr>
<tr><td> カタカナ入力モード </td><td> social-ime-katakana-key? </td></tr>
<tr><td> 半角カタカナ入力モード </td><td> social-ime-halfkana-key? </td></tr>
<tr><td> 半角英数字入力モード </td><td> social-ime-halfwidth-alnum-key? </td></tr>
<tr><td> 全角英数字モード </td><td> social-ime-fullwidth-alnum-key? </td></tr>
<tr><td> ひらがな/カタカナ入力モードを反転 </td><td> social-ime-kana-toggle-key? </td></tr>
<tr><td> かな/英数入力モードを反転 </td><td> social-ime-alkana-toggle-key? </td></tr>
<tr><td> Next prediction candidate </td><td> social-ime-next-prediction-key? </td></tr>
<tr><td> Previous prediction candidate </td><td> social-ime-prev-prediction-key? </td></tr>