= uim-look =

## これは何？ ##

とてもちいさな予測変換入力方式。

## 使い方 ##

  1. あらかじめ[SCOWL辞書](http://wordlist.sourceforge.net/)などを入手しておいてください。予測変換入力に必要ですが、これはuimに含まれていません。
  1. [UimPref](UimPref.md)を起動してください。
    * [UimToolbar](UimToolbar.md)の設定アイコンをクリック
    * ターミナルエミュレータなどでuim-pref-gtk（もしくはuim-pref-qt）を実行
  1. 「Look」→「[Look](Look.md) lookで使用される辞書ファイル名」の「選択...」ボタンを押して、辞書ファイルを指定します。
  1. [UimImSwitcher](UimImSwitcher.md)や[UimToolbar](UimToolbar.md)からLookに切り換えてください。
    1. Lookが見つからない場合は[UimPref](UimPref.md)を起動してください。
    1. 起動したら、「全体設定」→「入力方式の利用準備」→「使用可能にする入力方式」の「編集...」ボタンを押して、左の有効アイテムにLookを追加してください。
      * そこにもLookが見つからない場合、uim-lookはインストールされていないのかもしれません。確認してみてください。
    1. 追加が完了したら、Lookで入力したいアプリケーションを再起動してください。
  1. [UimImSwitcher](UimImSwitcher.md)や[UimToolbar](UimToolbar.md)による切り換えは一時的なものです。永続的な変更を望むなら[UimPref](UimPref.md)で設定する必要があります。
  1. [UimPref](UimPref.md)を起動したら、「全体設定」→「入力方式の利用準備」→「標準の入力方式を指定」のチェックボックスにチェックを入れます。
  1. そのすぐ下の「標準の入力方式」に、Lookをセットしてください。

### サポートしている入力モード ###

  * Look休眠入力モード
  * 直接入力モード
  * Look入力モード

### 標準で指定されているキー設定 ###

| 動作 | キー |
|:---|:---|
| オン/オフ | 全角/半角、Shift+Space |
| 補完 | Tab、End、Ctrl+e |
| 次の文字 | →、Ctrl+f |
| 次の文字 | BS、Ctrl+h、←、Ctrl+b |
| 次の予測候補へ | ↓、Ctrl+n |
| 前の予測候補へ | ↑、Ctrl+p |
| 辞書の保存 | Ctrl+s、Return |
| 辞書の読み出し | Ctrl+l |

### ファイル ###

~/.uim.d/custom/custom-look.scm:: [UimPref](UimPref.md)の「Look」ファイル。~/.uim.d/custom/custom-look-keys.scm:: [UimPref](UimPref.md)の「Look キー設定」ファイル。~/.look-uim-dict:: 個人辞書ファイル。

## カスタマイズ可能な項目 ##

### Lookの変数 ###

| 動作 | 変数名 | 指定できる値 | 標準値 |
|:---|:----|:-------|:----|
| [Look](Look.md) lookで使用される辞書ファイル名 | look-dict | "文字列"  | "/usr/share/dict/words" |
| [Look](Look.md) 個人辞書ファイル | look-personal-dict-filename | "文字列"  | "$HOME/.look-uim-dict" |
| [Look](Look.md) 予測入力が有効になる文字数 | look-beginning-character-length | 数字     | 1   |
| [Look](Look.md) 予測入力の学習に必要とする連接単語数 | look-prepered-words | 数字     | 0   |
| [Look](Look.md) 候補の左側のフェンス文字 | look-fence-left | "文字列"  | "{" |
| [Look](Look.md) 候補の右側のフェンス文字 | look-fence-right | "文字列"  |  "}" |

### Lookキー設定の変数 ###

| 動作 | キー変数名 |
|:---|:------|
| オン | look-on-key? |
| オフ | look-off-key? |
| 補完後確定 | look-completion-key? |
| 次の文字 | look-next-char-key? |
| 前の文字 | look-prev-char-key? |
| 次候補 | look-next-candidate-key? |
| 前候補 | look-prev-candidate-key? |
| 辞書の保存 | look-save-dict-key? |
| 辞書の読み出し | look-load-dict-key? |