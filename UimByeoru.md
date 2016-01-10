= uim-byeoru =



## これは何？ ##

uimのByeoruモジュール。 ハングル入力スイートByeoruで入力/変換などを行なう場合に使う。

## 使い方 ##

  1. [UimImSwitcher](UimImSwitcher.md)や[UimToolbar](UimToolbar.md)からByeoruに切り換えてください。
    1. Byeoruが見つからない場合は[UimPref](UimPref.md)を起動してください。
      * [UimToolbar](UimToolbar.md)の設定アイコンをクリック
      * ターミナルエミュレータなどでuim-pref-gtk（もしくはuim-pref-qt）を実行
    1. 起動したら、「全体設定」→「入力方式の利用準備」→「使用可能にする入力方式」の「編集...」ボタンを押して、左の有効アイテムにByeoruを追加してください。
      * そこにもByeoruが見つからない場合、uim-byeoruはインストールされていないのかもしれません。確認してみてください。
    1. 追加が完了したら、Byeoruで入力したいアプリケーションを再起動してください。
  1. [UimImSwitcher](UimImSwitcher.md)や[UimToolbar](UimToolbar.md)による切り換えは一時的なものです。永続的な変更を望むなら[UimPref](UimPref.md)で設定する必要があります。
  1. [UimPref](UimPref.md)を起動したら、「全体設定」→「入力方式の利用準備」→「標準の入力方式を指定」のチェックボックスにチェックを入れます。
  1. そのすぐ下の「標準の入力方式」に、Byeoruをセットしてください。

### サポートしている入力モード ###

このページはEUC-JPなので書けませんが、直訳で以下のようなモードをサポートしています。

  * 英文入力モード
  * ハングル字単位入力モード
  * ハングル単語単位入力モード

### サポートしているハングルキーボードのレイアウト ###

  * ハングル2ボル式 (Windows互換)
  * ハングル2ボル式 (Hanterm互換)
  * ハングル3ボル式最終版 (厳密)
  * ハングル3ボル式最終版 (寛容)
  * ハングル390式 (厳密)
  * ハングル390式 (寛容)
  * ハングル3ボル式 (シフトなし)
  * ハングルローマ字式

### 標準で指定されているキー設定 ###

| 動作 | キー |
|:---|:---|
| オン/オフ | Shift+Space |
| 右へ移動 | →、Ctrl+b |
| 左へ移動 | ←、Ctrl+f |
| 単語の先頭へ移動 | Home、Ctrl+a |
| 単語の末尾へ移動 | End、Ctrl+e |
| カーソルの右の一字を削除 | Delete、Ctrl+d |
| カーソルの左の一字を削除 | BS、Ctrl+h |
| 次の変換候補へ移動 | Space、↓、Ctrl+n |
| 前の変換候補へ移動 | ↑、Ctrl+p |
| 次の変換候補ページへ移動 | PgDn |
| 前の変換候補ページへ移動 | PgUp |
| 変換確定 | Ctrl+j、Enter、Ctrl+m |
| キャンセル | ESC、Ctrl+[、Ctrl+g |
| ハングルから漢字へ変換 | F9 |

### ファイル ###

~/.uim.d/customs/custom-byeoru.scm:: [UimPref](UimPref.md)の「Byeoru」ファイル。~/.uim.d/customs/custom-byeoru-keys(1,2).scm:: [UimPref](UimPref.md)の「Byeoru キー設定」ファイル。

## カスタマイズ可能な項目 ##

### Byeoruの変数 ###

| 動作 | 変数名 | 指定できる値 | 標準値 |
|:---|:----|:-------|:----|
| ハングルキーボードのレイアウト | byeoru-layout | 'byeoru-layout-hangul2<br> 'byeoru-layout-hangul2hanterm<br> 'byeoru-layout-strict3final<br> 'byeoru-layout-generous3final<br> 'byeoru-layout-strict390<br> 'byeoru-layout-generous390<br> 'byeoru-layout-no-shift<br> 'byeoru-layout-romaja <table><thead><th> 'byeoru-layout-hangul2 </th></thead><tbody>
<tr><td> 字母入力 </td><td> byeoru-jamo-orderedness </td><td> 'ordered<br> 'orderless<br> 'more-orderless </td><td> 'ordered </td></tr>
<tr><td> ESCキーでハングルモードをオフにする (viユーザ向け) </td><td> byeoru-esc-turns-off? </td><td> #t #f  </td><td> #t  </td></tr>
<tr><td> 標準の確定単位を単語にする </td><td> byeoru-commit-by-word? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> シフト+ローマ字母音で単母音を入力する </td><td> byeoru-shifted-romaja-isolates-vowel? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> 候補ウィンドウのサイズ </td><td> byeoru-nr-candidate-max </td><td> 数字     </td><td> 10  </td></tr>
<tr><td> 記号のキャッシュサイズ </td><td> define byeoru-symbol-cache-size </td><td> 数字     </td><td> 5   </td></tr>
<tr><td> 互換字母を使用して構成中の音節を表す </td><td> byeoru-compatibility-jamos-for-incomplete-syllables? </td><td> #t #f  </td><td> #t  </td></tr></tbody></table>

<h4>Byeoruの変数の依存関係</h4>

<ul><li>byeoru-layout 'byeoru-layout-hangul2 'byeoru-layout-hangul2hanterm 'byeoru-layout-strict3final 'byeoru-layout-strict390<br>
<ul><li>byeoru-jamo-orderedness<br>
</li><li>byeoru-shifted-romaja-isolates-vowel?</li></ul></li></ul>

<ul><li>byeoru-layout 'byeoru-layout-romaja<br>
<ul><li>byeoru-shifted-romaja-isolates-vowel?</li></ul></li></ul>

<ul><li>byeoru-layout 'byeoru-layout-generous3final 'byeoru-layout-generous390 'byeoru-layout-no-shift<br>
<ul><li>byeoru-shifted-romaja-isolates-vowel?</li></ul></li></ul>

<h3>Byeoruキー設定の変数</h3>

<table><thead><th> 動作 </th><th> キー変数名 </th></thead><tbody>
<tr><td> オン </td><td> byeoru-on-key? </td></tr>
<tr><td> オフ </td><td> byeoru-latin-key? </td></tr>
<tr><td> ハングルから漢字へ変換 </td><td> byeoru-conversion-key? </td></tr>
<tr><td> 変換確定 </td><td> byeoru-commit-key? </td></tr>
<tr><td> 変換キャンセル </td><td> byeoru-cancel-key? </td></tr>
<tr><td> 次候補 </td><td> byeoru-next-candidate-key? </td></tr>
<tr><td> 前候補 </td><td> byeoru-prev-candidate-key? </td></tr>
<tr><td> 候補ウィンドウの次ページ </td><td> byeoru-next-page-key? </td></tr>
<tr><td> 候補ウィンドウの前ページ </td><td> byeoru-prev-page-key? </td></tr>
<tr><td> バックスペース </td><td> byeoru-backspace-key? </td></tr>
<tr><td> デリート </td><td> byeoru-delete-key? </td></tr>
<tr><td> 左に移動 </td><td> byeoru-go-left-key? </td></tr>
<tr><td> 右に移動 </td><td> byeoru-go-right-key? </td></tr>
<tr><td> 単語の先頭 </td><td> byeoru-beginning-of-preedit-key? </td></tr>
<tr><td> 単語の末尾 </td><td> byeoru-end-of-preedit-key? </td></tr>