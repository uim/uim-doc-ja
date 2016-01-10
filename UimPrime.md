= uim-prime =



## これは何？ ##

uimの[PRIME](http://www.taiyaki.org/prime/)モジュール。 日本語/英語の予測変換入力方式PRIMEで入力/変換などを行なう場合に使う。

## 使い方 ##

  1. [UimImSwitcher](UimImSwitcher.md)や[UimToolbar](UimToolbar.md)からPRIMEに切り換えてください。
    1. PRIMEが見つからない場合は[UimPref](UimPref.md)を起動してください。
      * [UimToolbar](UimToolbar.md)の設定アイコンをクリック
      * ターミナルエミュレータなどでuim-pref-gtk（もしくはuim-pref-qt）を実行
    1. 起動したら、「全体設定」→「入力方式の利用準備」→「使用可能にする入力方式」の「編集...」ボタンを押して、左の有効アイテムにPRIMEを追加してください。
      * そこにもPRIMEが見つからない場合、uim-primeはインストールされていないのかもしれません。確認してみてください。
    1. 追加が完了したら、PRIMEで入力したいアプリケーションを再起動してください。
  1. [UimImSwitcher](UimImSwitcher.md)や[UimToolbar](UimToolbar.md)による切り換えは一時的なものです。永続的な変更を望むなら[UimPref](UimPref.md)で設定する必要があります。
  1. [UimPref](UimPref.md)を起動したら、「全体設定」→「入力方式の利用準備」→「標準の入力方式を指定」のチェックボックスにチェックを入れます。
  1. そのすぐ下の「標準の入力方式」に、PRIMEをセットしてください。

### サポートしている入力モード ###

  * 通常入力モード
  * 英語入力モード
  * 日本語入力モード
  * 全角英数入力モード
  * 特殊入力モード

### サポートしているかな入力方式 ###

PRIMEでは[suikyo](http://taiyaki.org/suikyo/)を利用しており、uimが持つ変換用テーブルは使われません。 かな入力方式を変更するには、PRIME側の設定を変更する必要があります。 詳しくは[PRIME の使い方](http://taiyaki.org/prime/usage.html)を参照してください。

  * ローマ字入力方式
  * AZIK拡張ローマ字入力方式
  * かな入力方式
  * T-Code入力方式
  * TUT-Code入力方式

### 標準で指定されているキー設定 ###

| 動作 | キー |
|:---|:---|
| オン | 全角/半角、Shift+Space、Ctrl+j |
| オフ | 全角/半角、Shift+Space、Ctrl+l |
| 全角英数入力モードへ移行 | Ctrl+L |
| カーソルを右へ移動 | →、Ctrl+f |
| カーソルを左へ移動 | ←、Ctrl+b |
| 編集領域の先頭へ移動 | Ctrl+a、Ctrl+← |
| 編集領域の末尾へ移動 | Ctrl+e、Ctrl+→ |
| カーソルの右の一字を削除 | Delete、Ctrl+d |
| カーソルの左の一字を削除 | BS、Ctrl+h |
| 変換開始 | Space |
| 次の変換候補へ移動 | Space、↓、Ctrl+n |
| 前の変換候補へ移動 | ↑、Ctrl+p |
| 次の変換候補ページへ移動 | PgDn |
| 前の変換候補ページへ移動 | PgUp |
| 変換確定 | Return、Ctrl+m、Ctrl+j |
| キャンセル | Esc、Ctrl+[、Ctrl+g |
| ひらがなへ変換 | F6 |
| カタカナへ変換 | F7 |
| 半角カタカナへ変換 | F8 |
| 全角英数字へ変換 | F9 |
| 半角英数字へ変換 | F10 |
| 言語切り換え | F11 |
| 全角半角を反転した空白文字を入力 | Ctrl+Space、Alt+Space |
| 単語登録 | Ctrl+w |

### vi協調モード ###

vi（クローン）でコマンドモードに戻る時、uimを直接入力モードに戻すことができます。

[UimPref](UimPref.md)で「PRIME (高度)」→「vi協調モードを有効にする」のチェックボックスにチェックを入れてください。

標準のキー設定は以下のようになっています。

| 動作 | キー |
|:---|:---|
| vi協調モードでESCとして扱うキー | ESC、Ctrl+[ |

### ファイル ###

~/.uim.d/customs/custom-prime.scm:: [UimPref](UimPref.md)の「PRIME」ファイル。~/.uim.d/customs/custom-prime-advanced.scm:: [UimPref](UimPref.md)の「PRIME (高度)」ファイル。~/.uim.d/customs/custom-prime-keys{1,2,3}.scm:: [UimPref](UimPref.md)の「PRIME キー設定{1,2,3}」ファイル。~/.uim.d/socket/uim-prime:: ソケットファイル。

## カスタマイズ可能な項目 ##

### PRIMEの変数 ###

| 動作 | 変数名 | 指定できる値 | 標準値 |
|:---|:----|:-------|:----|
| 標準の言語 | prime-custom-default-language | 'Japanese<br> 'English <table><thead><th> 'Japanese </th></thead><tbody>
<tr><td> 言語切り換えキー </td><td> prime-language-toggle-key </td><td> '("キー") </td><td> '("F11") </td></tr>
<tr><td> 自動登録モードを有効にする </td><td> prime-auto-register-mode? </td><td> #t #f  </td><td> #t  </td></tr>
<tr><td> 空白文字 </td><td> prime-custom-japanese-space </td><td> 'wide<br> 'half </td><td> 'wide </td></tr>
<tr><td> 全角半角を反転した空白文字キー </td><td> prime-altspace-key </td><td> '("キー") </td><td> '("<br>
<br>
<Control><br>
<br>
 " "<br>
<br>
<Alt><br>
<br>
 ") </td></tr>
<tr><td> PRIMEとの通信にUNIXドメインソケットを使用する </td><td> prime-use-unixdomain? </td><td> #t #f  </td><td> #t  </td></tr>
<tr><td> 候補ウィンドウに一度に表示する候補数 </td><td> prime-nr-candidate-max </td><td> 数字     </td><td> 10  </td></tr>
<tr><td> 常に候補ウィンドウを表示する </td><td> prime-always-show-window? </td><td> #t #f  </td><td> #t  </td></tr>
<tr><td> 候補単語の用例を表示 </td><td> prime-custom-display-usage? </td><td> #t #f  </td><td> #t  </td></tr>
<tr><td> 候補単語の註釈を表示 </td><td> prime-custom-display-comment? </td><td> #t #f  </td><td> #t  </td></tr>
<tr><td> 候補単語の活用形を表示 </td><td> prime-custom-display-form? </td><td> #t #f  </td><td> #t  </td></tr>
<tr><td> 数字キーで候補を選択する </td><td> prime-custom-number-selection? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> vi協調モードを有効にする </td><td> prime-custom-app-mode-vi? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> 擬似モードカーソルを有効にする </td><td> prime-pseudo-mode-cursor? </td><td> #t #f  </td><td> #f  </td></tr></tbody></table>

<h3>PRIMEキー設定の変数</h3>

<table><thead><th> 動作 </th><th> キー変数名 </th></thead><tbody>
<tr><td> 単語登録キー </td><td> prime-register-key? </td></tr>
<tr><td> 入力モードのひらがなキー </td><td> prime-typing-mode-hiragana-key? </td></tr>
<tr><td> 入力モードのカタカナキー </td><td> prime-typing-mode-katakana-key? </td></tr>
<tr><td> 入力モードの半角カタカナキー </td><td> prime-typing-mode-hankana-key? </td></tr>
<tr><td> 入力モードの全角英数字キー </td><td> prime-typing-mode-wideascii-key? </td></tr>
<tr><td> 入力モードの半角英数字キー </td><td> prime-typing-mode-ascii-key? </td></tr>
<tr><td> オン </td><td> prime-on-key? </td></tr>
<tr><td> オフ </td><td> prime-latin-key? </td></tr>
<tr><td> 全角英数字モード </td><td> prime-wide-latin-key? </td></tr>
<tr><td> 変換開始 </td><td> prime-begin-conv-key? </td></tr>
<tr><td> 確定 </td><td> prime-commit-key? </td></tr>
<tr><td> キャンセル </td><td> prime-cancel-key? </td></tr>
<tr><td> 次候補 </td><td> prime-next-candidate-key? </td></tr>
<tr><td> 前候補 </td><td> prime-prev-candidate-key? </td></tr>
<tr><td> 候補ウィンドウの次ページ </td><td> prime-next-page-key? </td></tr>
<tr><td> 変換ウィンドウの前ページ </td><td> prime-prev-page-key? </td></tr>
<tr><td> 編集領域の先頭 </td><td> prime-go-left-edge-key? </td></tr>
<tr><td> 編集領域の末尾 </td><td> prime-go-right-edge-key? </td></tr>
<tr><td> バックスペース </td><td> prime-backspace-key? </td></tr>
<tr><td> デリート </td><td> prime-delete-key? </td></tr>
<tr><td> 左に移動 </td><td> prime-go-left-key? </td></tr>
<tr><td> 右に移動 </td><td> prime-go-right-key? </td></tr>
<tr><td> 英語モードでの次候補 </td><td> prime-english-next-candidate-key? </td></tr>
<tr><td> 英語モードでの直接入力キー </td><td> prime-english-direct-key? </td></tr>