= uim-skk =



## これは何？ ##

[SKK](http://openlab.jp/skk/index-j.html)入力方式のuim版。

## 使い方 ##

  1. あらかじめ[SKK辞書](http://openlab.ring.gr.jp/skk/dic/)などを入手しておいてください。漢字変換に必要ですが、これはuimに含まれていません。
  1. [UimPref](UimPref.md)を起動してください。
    * [UimToolbar](UimToolbar.md)の設定アイコンをクリック
    * ターミナルエミュレータなどでuim-pref-gtk（もしくはuim-pref-qt）を実行
  1. 「SKK 辞書」→「辞書ファイル」→「システム辞書ファイル」の「選択...」ボタンを押して、辞書ファイルを指定します。
  1. [UimImSwitcher](UimImSwitcher.md)や[UimToolbar](UimToolbar.md)からSKKに切り換えてください。
    1. SKKが見つからない場合は[UimPref](UimPref.md)を起動してください。
    1. 起動したら、「全体設定」→「入力方式の利用準備」→「使用可能にする入力方式」の「編集...」ボタンを押して、左の有効アイテムにSKKを追加してください。
      * そこにもSKKが見つからない場合、uim-skkはインストールされていないのかもしれません。確認してみてください。
    1. 追加が完了したら、SKKで入力したいアプリケーションを再起動してください。
  1. [UimImSwitcher](UimImSwitcher.md)や[UimToolbar](UimToolbar.md)による切り換えは一時的なものです。永続的な変更を望むなら[UimPref](UimPref.md)で設定する必要があります。
  1. [UimPref](UimPref.md)を起動したら、「全体設定」→「入力方式の利用準備」→「標準の入力方式を指定」のチェックボックスにチェックを入れます。
  1. そのすぐ下の「標準の入力方式」に、SKKをセットしてください。

### サポートしている入力モード ###

  * 直接入力モード
  * ひらがな入力モード
  * カタカナ入力モード
  * 半角カタカナ入力モード
  * 全角英数字入力モード

### サポートしているかな入力方式 ###

  * [ローマ字入力方式](RomaKanaTable.md)
  * [AZIK拡張ローマ字入力方式](AZIKTable.md)
  * ACT拡張ローマ字入力方式
  * KZIK拡張ローマ字入力方式

### 標準で指定されているキー設定 ###

| 動作 | キー |
|:---|:---|
| 直接/全角英数字入力モードからひらがな入力モードへ移行 | 全角/半角、Shift+Space、Ctrl+j |
| ひらがな/カタカナ/半角カタカナ入力モードから直接入力モードへ移行 | 全角/半角、Shift+Space、l |
| ひらがな/カタカナ入力モードを反転移行 | q  |
| ひらがな/カタカナ入力モードから半角カタカナ入力モードへ移行 | Ctrl+q |
| 半角カタカナ入力モードからひらがな入力モードへ移行 | q  |
| ひらがな/カタカナ/半角カタカナ入力モードから全角英数字入力モードへ移行 | L  |
| ひらがな/カタカナ/半角カタカナ入力モードから漢字入力モードへ移行 | Q  |
| 漢字コード入力 | \  |
| カーソルを右へ移動 | →、Ctrl+f |
| カーソルを左へ移動 | ←、Ctrl+b |
| カーソルの左の一字を削除 | BS、Ctrl+h |
| 変換開始 | Space |
| 次の候補へ移動 | Space、↓、Ctrl+n |
| 前の候補へ移動 | ↑、Ctrl+p、x |
| 次の変換候補ページへ移動 | Space、↓、Ctrl+n、PgDn |
| 前の変換候補ページへ移動 | ↑、Ctrl+p、x、PgUp |
| 変換確定 | Ctrl+m、Ctrl+j |
| 変換確定+改行 | Return |
| 候補ウィンドウから変換候補を選択し確定 | a、s、d、f、g、h、j、k、l |
| キャンセル | Esc、Ctrl+[、Ctrl+g |
| ひらがな/カタカナを反転変換し確定 | q  |
| ひらがな/カタカナを半角カタカナとして確定 | Ctrl+q |
| ひらがな/カタカナ/半角カタカナ入力モードでアルファベット変換開始 | /  |
| アルファベット変換中に全角英数字として確定 | Ctrl+q |
| アルファベット変換中に大文字/小文字を反転変換し確定 | Ctrl+u |
| 編集領域を補完 | Tab、Ctrl+i、Alt+Tab、Ctrl+Alt+i |
| 次の補完候補へ移動 | .、Tab、Ctrl+i、Alt+Tab、Ctrl+Alt+i |
| 前の補完候補へ移動 | ,  |
| 補完候補から新規に補完 | Alt+Tab、Ctrl+Alt+i |
| 接頭辞/接尾辞入力 | >、<、? |
| 個人辞書中の単語を削除 | X  |

### SKKサーバを利用する ###

localhost以外のSKKサーバを利用するには、環境変数'''SKKSERVER'''にホスト名かIPアドレスを指定してください。

[UimPref](UimPref.md)で「SKK辞書」→「辞書ファイルの代わりにSKKサーバを使用」のチェックボックスにチェックを入れてください。

### 自動ダイナミックコンプリーションを使う ###

補完の第一候補をインクリメンタルに表示します。

[UimPref](UimPref.md)で「SKK (高度)」→「動的補完を有効にする」のチェックボックスにチェックを入れてください。

標準のキー設定は以下のようになっています。

| 動作 | キー |
|:---|:---|
| 動的補完された語を変換開始 | Alt+Space |
| 動的補完された語を変換し確定 | Ctrl+Alt+j |

### vi協調モード ###

vi（クローン）でコマンドモードに戻る時、uimを直接入力モードに戻すことができます。

[UimPref|UimPref]で「SKK (高度)」→「特殊操作」→「vi協調モードを有効にする」のチェックボックスにチェックを入れてください。

標準のキー設定は以下のようになっています。

| 動作 | キー |
|:---|:---|
| vi協調モードでESCとして扱うキー | ESC、Ctrl+[ |

### 改行をネイティブキーイベントの代わりにASCII文字列として確定する ###

詳しくは[691](http://lists.sourceforge.jp/mailman/archives/anthy-dev/2004-March/000690.html|Anthy-dev)を。

### 漢字コード入力 ###

漢字コード入力後確定キーを押すと、対応する文字が確定されます。
以下の3種類の形式での入力が可能(DDSKK 14.2と同様)。

  * Unicode(UCS): U+の後に16進数。U+のかわりにuでもOK(例:U+4E85またはu4e85)。(ただし、uim-skkの内部コードはEUC-JP(EUC-JIS-2004)なので、JIS X 0213に無い文字(例:はしご高U+9AD9)は入力不可)
  * 区点番号(JIS X 0213): -で区切った、面-区-点番号(面区点それぞれ10進数)。1面の場合、面-は省略可能。(例:1-48-13または48-13)
  * JISコード(ISO-2022-JP): 4桁の16進数。(例:502d)

### ファイル ###

~/.uim.d/customs/custom-skk.scm:: [UimPref|UimPref]の「SKK」ファイル。~/.uim.d/customs/custom-skk-dict.scm:: [UimPref|UimPref]の「SKK 辞書」ファイル。~/.uim.d/customs/custom-skk-advanced.scm:: [UimPref|UimPref]の「SKK (高度)」ファイル。~/.uim.d/customs/custom-skk-keys{1,2,3}.scm:: [UimPref|UimPref]の「SKK キー設定{1,2,3}」ファイル。~/.skk-uim-jisyo:: 個人辞書(uim専用)ファイル。~/.skk-uim-jisyo.lock:: 個人辞書(uim専用)のロックファイル。

### 環境変数 ###

SKKSERVER

## カスタマイズ可能な項目 ##

### SKKの変数 ###

| 動作 | 変数名 | 指定できる値 | 標準値 |
|:---|:----|:-------|:----|
| 候補ウィンドウを使用する | skk-use-candidate-window? | #t #f  | #t  |
| 見出し表示のキーで候補を確定する | skk-commit-candidate-by-label-key? | #t #f  | #t  |
| 候補選択のスタイル | skk-candidate-selection-style | 'ddskk-like<br> 'uim <table><thead><th> 'ddskk-like </th></thead><tbody>
<tr><td> 候補ウィンドウの挙動を手動で設定する </td><td> skk-use-manual-candwin-setting? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> 候補ウィンドウを表示するために変換キーを押す回数 </td><td> skk-candidate-op-count </td><td> 数字     </td><td> 5   </td></tr>
<tr><td> 候補ウィンドウに一度に表示する候補数 </td><td> skk-nr-candidate-max </td><td> 数字     </td><td> 7   </td></tr>
<tr><td> 標準の入力モード </td><td> default-widget_skk_input_mode </td><td> 'action_skk_latin<br> 'action_skk_hiragana<br> 'action_skk_katakana<br> 'action_skk_hankana<br> 'action_skk_wide_latin </td><td> 'action_skk_latin </td></tr>
<tr><td> 標準のかな入力方式 </td><td> default-widget_skk_kana_input_method </td><td> 'action_skk_roma<br> 'action_skk_azik </td><td> 'action_skk_roma </td></tr>
<tr><td> 辞書ファイルの代わりにSKKサーバを使用 </td><td> skk-use-skkserv? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> skkserv補完を有効にする </td><td> skk-skkserv-enable-completion? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> skkserv補完のタイムアウト時間 (msec) </td><td> skk-skkserv-completion-timeout </td><td> 数字     </td><td> 2000 </td></tr>
<tr><td> 環境変数SKKSERVERを使用 </td><td> skk-skkserv-use-env? </td><td> #t #f  </td><td> #t  </td></tr>
<tr><td> SKKサーバのホスト名 </td><td> skk-skkserv-hostname </td><td> "文字列"  </td><td> "localhost" </td></tr>
<tr><td> SKKサーバのポート番号 </td><td> skk-skkserv-portnum </td><td> 数字     </td><td> 1178 </td></tr>
<tr><td> SKKサーバのアドレスファミリ </td><td> skk-skkserv-address-family </td><td> 'unspecified<br> 'inet<br> 'inet6 </td><td> 'unspecified </td></tr>
<tr><td> システム辞書ファイル </td><td> skk-dic-file-name </td><td> "文字列"  </td><td> /usr/local/share/skk/SKK-JISYO.L" </td></tr>
<tr><td> 個人辞書ファイル </td><td> skk-personal-dic-filename </td><td> "文字列"  </td><td> "$HOME/.skk-jisyo" </td></tr>
<tr><td> 個人辞書ファイル (uim専用) </td><td> skk-uim-personal-dic-filename </td><td> "文字列"  </td><td> "$HOME/.skk-uim-jisyo" </td></tr>
<tr><td> ビジュアルスタイル </td><td> skk-style </td><td> 'skk-style-ddskk-like<br> 'skk-style-uim </td><td> 'skk-style-ddskk-like </td></tr>
<tr><td> 再帰学習を使用する </td><td> skk-use-recursive-learning? </td><td> #t #f  </td><td> #t  </td></tr>
<tr><td> 数値変換を使用する </td><td> skk-use-numeric-conversion? </td><td> #t #f  </td><td> #t  </td></tr>
<tr><td> 句読点での自動変換を有効にする </td><td> skk-auto-start-henkan? </td><td> #t #f  </td><td> #t  </td></tr>
<tr><td> 動的補完を有効にする </td><td> skk-dcomp-activate? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> アルファベット変換時の補完にlookコマンドを使用 </td><td> skk-use-look? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> UNIX look辞書ファイル </td><td> skk-look-dict </td><td> "文字列"  </td><td> "/usr/share/dict/words" </td></tr>
<tr><td> 候補の注釈を表示する </td><td> skk-show-annotation? </td><td> #t #f  </td><td> #t  </td></tr>
<tr><td> 編集領域内にも注釈を表示する </td><td> skk-show-annotation-in-preedit? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> vi協調モードを有効にする </td><td> skk-use-with-vi? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> Enterキーを単に確定のために使う (egg風の操作) </td><td> skk-egg-like-newline? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> 改行をネイティブキーイベントの代わりにASCII文字列として確定する </td><td> skk-commit-newline-explicitly? </td><td> #t #f  </td><td> #f  </td></tr></tbody></table>

<h4>SKKの変数の依存関係</h4>

<ul><li>skk-use-candidate-window? #f<br>
<ul><li>skk-commit-candidate-by-label-key?<br>
</li><li>skk-candidate-selection-style<br>
</li><li>skk-use-manual-candwin-setting?</li></ul></li></ul>

<ul><li>skk-candidate-selection-style 'uim 'ddskk<br>
<ul><li>skk-candidate-op-count<br>
</li><li>skk-nr-candidate-max</li></ul></li></ul>

<ul><li>skk-use-manual-candwin-setting? #f<br>
<ul><li>skk-candidate-op-count<br>
</li><li>skk-nr-candidate-max</li></ul></li></ul>

<ul><li>skk-use-skkserv? #f<br>
<ul><li>skk-skkserv-use-env?<br>
</li><li>skk-skkserv-portnum<br>
</li><li>skk-skkserv-address-family<br>
</li><li>skk-skkserv-enable-completion?</li></ul></li></ul>

<ul><li>skk-skkserv-enable-completion? #f<br>
<ul><li>skk-skkserv-completion-timeout</li></ul></li></ul>

<ul><li>skk-use-skkserv? #t<br>
<ul><li>skk-dic-file-name</li></ul></li></ul>

<ul><li>skk-skkserv-use-env? #t<br>
<ul><li>skk-skkserv-hostname</li></ul></li></ul>

<ul><li>skk-use-look? #f<br>
<ul><li>skk-look-dict</li></ul></li></ul>

<ul><li>skk-show-annotation? #f<br>
<ul><li>skk-show-annotation-in-preedit?</li></ul></li></ul>

<h3>SKKキー設定の変数</h3>

<table><thead><th> 動作 </th><th> キー変数名 </th></thead><tbody>
<tr><td> オン </td><td> skk-on-key? </td></tr>
<tr><td> 半角英数入力モード </td><td> skk-latin-key? </td></tr>
<tr><td> 全角英数入力モード </td><td> skk-wide-latin-key? </td></tr>
<tr><td> 漢字コード入力モード </td><td> skk-kcode-input-key? </td></tr>
<tr><td> 漢字入力モード </td><td> skk-kanji-mode-key? </td></tr>
<tr><td> 半角カタカナ入力モード </td><td> skk-hankaku-kana-key? </td></tr>
<tr><td> ひらがな/カタカナ入力モードを反転 </td><td> skk-kana-toggle-key? </td></tr>
<tr><td> 変換開始 </td><td> skk-begin-conv-key? </td></tr>
<tr><td> 確定 </td><td> skk-commit-key? </td></tr>
<tr><td> キャンセル </td><td> skk-cancel-key? </td></tr>
<tr><td> リターン </td><td> skk-return-key? </td></tr>
<tr><td> 接頭辞、接尾辞の入力 </td><td> skk-special-midashi-key? </td></tr>
<tr><td> vi協調モードでESCとして扱うキー </td><td> skk-vi-escape-key? </td></tr>
<tr><td> 編集領域がない時に何もせずに消費するキー </td><td> skk-state-direct-no-preedit-nop-key? </td></tr>
<tr><td> 個人辞書中の単語を削除 </td><td> skk-purge-candidate-key? </td></tr>
<tr><td> アルファベット変換開始 </td><td> skk-latin-conv-key? </td></tr>
<tr><td> 全角英数字として確定 </td><td> skk-conv-wide-latin-key? </td></tr>
<tr><td> 大文字/小文字を反転して確定 </td><td> skk-conv-opposite-case-key? </td></tr>
<tr><td> 補完開始 </td><td> skk-begin-completion-key? </td></tr>
<tr><td> 次の補完候補 </td><td> skk-next-completion-key? </td></tr>
<tr><td> 前の補完候補 </td><td> skk-prev-completion-key? </td></tr>
<tr><td> 現在の補完候補から新規に補完 </td><td> skk-new-completion-from-current-comp-key? </td></tr>
<tr><td> 動的補完された語を変換開始 </td><td> skk-begin-conv-with-completion-key? </td></tr>
<tr><td> 動的補完された語を変換、確定 </td><td> skk-commit-with-conv-completion-key? </td></tr>
<tr><td> 次候補 </td><td> skk-next-candidate-key? </td></tr>
<tr><td> 前候補 </td><td> skk-prev-candidate-key? </td></tr>
<tr><td> 候補ウィンドウの次のページ </td><td> skk-next-page-key? </td></tr>
<tr><td> 候補ウィンドウの前のページ </td><td> skk-prev-page-key? </td></tr>
<tr><td> バックスペース </td><td> skk-backspace-key? </td></tr>
<tr><td> 左に移動 </td><td> skk-go-left-key? </td></tr>
<tr><td> 右に移動 </td><td> skk-go-right-key? </td></tr>