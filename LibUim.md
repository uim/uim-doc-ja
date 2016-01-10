= libuim =



## これは何？ ##

uimライブラリ。 1.4.0以降では、Schemeインタープリタ[SigScheme](http://code.google.com/p/sigscheme/)が内蔵されています。

## 使い方 ##

以下は明示的に有効にされています。

  * enable EUC-JP character encoding

以下は明示的に無効にされています。

  * disable building libsscm
  * disable the 'sscm' interactive shell

### ファイル ###

~/.uim.d/customs/custom-global.scm:: [UimPref](UimPref.md)の「全体設定」ファイル。

~/.uim.d/customs/custom-global-keys{1,2}.scm:: [UimPref](UimPref.md)の「全体キー設定{1,2}」ファイル。

~/.uim.d/customs/custom-other-ims.scm:: [UimPref](UimPref.md)の「その他の入力方式」ファイル。

~/.uim.d/customs/custom-notify.scm:: [UimPref](UimPref.md)の「状態通知」ファイル。

### 環境変数 ###

LIBUIM\_VERBOSE:: メッセージの冗長レベルを'''0'''から'''10'''まで指定できます。'''3'''を指定するとファイルの読み込み状況を出力。'''4'''を指定するとGCの利用状況を出力。'''5'''以上を指定するとコードの評価過程を出力し、エラーがいつ発生したのかバックトレースを表示します。この環境変数を利用するにはuimを'''--enable-debug'''と'''--enable-backtrace'''でビルドする必要があります。

LIBUIM\_ENABLE\_EMERGENCY\_KEY:: emergency keyを有効にします。この環境変数をブリッジの起動前に指定すると、Shift+BSを押す事でuimのキー処理をすべて無効にできるようになります。

LIBUIM\_VANILLA:: 2を指定すると、設定ファイル（/usr/local/share/uim/default.scmや ~/.uim、~/.uim.dなど）を無視、遅延ローディングを無効にします。それ以外を指定すると、設定ファイル（/usr/local/share/uim/default.scmや~/.uim、~/.uim.dなど）を無視、遅延ローディングを無効、direct以外のモジュールを読み込まなくなります。

LIBUIM\_SCM\_FILES:: Schemeファイルを置くディレクトリをコロンで区切ったパスで指定します。標準では$prefix/share/uimです。

LIBUIM\_USER\_SCM\_FILE:: ユーザーの設定ファイルを指定します。標準では~/.uimです。

LIBUIM\_PLUGIN\_LIB\_DIR:: ダイナミックライブラリファイルを置くディレクトリを指定します。
読込みパスの優先順序は、LIBUIM\_PLUGIN\_LIB\_DIR, ~/.uim.d/plugin, $pkglibdir/uim/plugin の順番になります。

UIM\_IM\_ENGINE:: 入力方式名を指定します。この環境変数を利用するにはuimを'''--enable-debug'''でビルドする必要があります。

## カスタマイズ可能な項目 ##

### 全体設定の変数 ###

| 動作 | 変数名 | 指定できる値 | 標準値 |
|:---|:----|:-------|:----|
|< 2> 標準の入力方式を指定   < 2> custom-activate-default-im-name? | #t   < 2> #f |
| #f |
|< 2> 標準の入力方式   < 2> default-im-name | 'IM名   < 2> #f |
| #f |
|< 2> 使用可能にする入力方式   < 2> enabled-im-list | 'IM名   < 2> 任意 |
| '(IM名 IM名) |
|< 2> ホットキーによる入力方式の一時切り換えを有効にする   < 2> enable-im-switch | #t   < 2> #f |
| #f |
| 一時切り換えキー | switch-im-key | '("キー") | '("

&lt;Control&gt;

Shift\_key" "

&lt;Shift&gt;

Control\_key") |
|< 2> 直接入力方式を飛ばして切り換える   < 2> switch-im-skip-direct-im? | #t   < 2> #f |
| #f |
|< 2> 入力方式の正副一時切り換え   < 2> enable-im-toggle? | #t   < 2> #t |
| #f |
| 一時切り換えキー | toggle-im-key | '("キー") | '("

&lt;Meta&gt;

 ") |
| 副入力方式 | toggle-im-alt-im | 'IM名   | 'direct |
|< 2> 編集領域の配色   < 2> uim-color | 'uim-color-uim   < 2> 'uim-color-uim |
| 'uim-color-atok |
|< 3> 候補ウィンドウの表示位置   < 3> candidate-window-position | 'caret   < 3> 'caret |
| 'left |
| 'right |
|< 2> 高速起動のための遅延ローディングを有効にする   < 2> enable-lazy-loading? | #t   < 2> #t |
| #f |
|< 2> カーソルの側に入力モードを表示する   < 2> bridge-show-input-state? | #t   < 2> #f |
| #f |
| カーソルの側に入力モードを表示する時間 | bridge-show-input-state-time-length | 数字     | 3   |

#### 全体設定の変数の依存関係 ####

  * custom-activate-default-im-name? #f
    * custom-preserved-default-im-name
    * default-im-name

  * enable-im-switch #f
    * switch-im-skip-direct-im?

  * enable-im-toggle? #f
    * toggle-im-key
    * toggle-im-alt-im

  * bridge-show-input-state? #f
    * bridge-show-input-state-time-length

### 状態通知の変数 ###

| 動作 | 変数名 | 指定できる値 | 標準値 |
|:---|:----|:-------|:----|
|< 4> 状態通知に使用するエージェント   < 4> notify-agent | 'stderr   < 4> 'stderr |
| 'libnotify |
| 'knotify3 |

### その他の入力方式の変数 ###

| 動作 | 変数名 | 指定できる値 | 標準値 |
|:---|:----|:-------|:----|
|< 2> 候補ウィンドウを使用する   < 2> generic-use-candidate-window? | #t   < 2> #t |
| #f |
| 候補ウィンドウの表示を開始するために変換キーを押す回数 | generic-candidate-op-count   < 2> 数字 | 1      |
| 候補ウィンドウに一度に表示する候補数 | generic-nr-candidate-max | 10     |
|< 2> 数字キーで候補を選択する   < 2> generic-commit-candidate-by-numeral-key? | #t   < 2> #t |
| #f |

#### その他の入力方式の変数の依存関係 ####

  * generic-use-candidate-window? #f
    * generic-candidate-op-count
    * generic-nr-candidate-max
    * generic-commit-candidate-by-numeral-key?

### 全体キー設定の変数 ###

| 動作 | キー変数名 |
|:---|:------|
| オン | generic-on-key? |
| オフ | generic-off-key? |
| 変換開始 | generic-begin-conv-key? |
| 確定 | generic-commit-key? |
| キャンセル | generic-cancel-key? |
| 次候補 | generic-next-candidate-key? |
| 前候補 | generic-prev-candidate-key? |
| 候補ウィンドウの次ページ | generic-next-page-key? |
| 候補ウィンドウの前ページ | generic-prev-page-key? |
| 編集領域の先頭 | generic-beginning-of-preedit-key? |
| 編集領域の末尾 | generic-end-of-preedit-key? |
| カーソル以降を消去 | generic-kill-key? |
| カーソル以前を消去 | generic-kill-backward-key? |
| バックスペース | generic-backspace-key? |
| デリート | generic-delete-key? |
| 左に移動 | generic-go-left-key? |
| 右に移動 | generic-go-right-key? |
| リターン | generic-return-key? |
