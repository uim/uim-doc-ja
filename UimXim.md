= uim-xim =

## これは何？ ##

![http://freedesktop.org/~ekato/img/xfig-uim-xim.png](http://freedesktop.org/~ekato/img/xfig-uim-xim.png)

uimとXIMのブリッジ。 XIM経由で入力を行う場合に使う。

## 使い方 ##

環境変数'''XMODIFIERS'''に'''@im=uim'''を指定して、uim-ximを起動する。 通常は、環境に合わせて~/.xsession、~/.xinitrc、~/.gnomerc、~/.xprofileあたりに

```
XMODIFIERS="@im=uim" ; export XMODIFIERS
uim-xim &
```

を追記しておくだけでよいでしょう。

### 候補ウィンドウ ###

GTK+ツールキットを用いたuim-candwin-gtkと、Qtツールキットを用いたuim-candwin-qt4とuim-candwin-qtが用意されていますが、どれもインストールされていない場合、候補ウィンドウを表示できません。 この場合、「候補ウィンドウを表示するために変換キーを押す回数」を0にすることで、編集領域から候補が消えてしまうのを回避できます。

```
;; 例 uim-anthyの場合
(define anthy-candidate-op-count 0)
```

環境変数'''UIM\_CANDWIN\_PROG'''を指定する事で、使用する候補ウィンドウを選択できます。

```
$ UIM_CANDWIN_PROG=uim-candwin-qt uim-xim &
```

### オプション ###

--async:: on-demand-synchronous methodモードで起動します。アプリがXIM\_ERRORを出す場合は、このオプションを試してみてください。このオプションをつけると、Tcl/Tk 8.3/8.4を利用したアプリでうまく動かなります。--engine=''入力方式名'':: 利用する入力方式を指定します。--list:: 利用可能な入力方式のリストを表示します。--trace:: --trace-xim:: --help, --version:: ヘルプやバージョンを表示します。

### ファイル ###

~/.uim.d/customs/custom-xim.scm:: [UimPref](UimPref.md)の「XIM」ファイル。

### 環境変数 ###

XMODIFIERS

UIM\_CANDWIN\_PROG

XCOMPOSEFILE

## カスタマイズ可能な項目 ##

### XIM設定の変数 ###

| 動作 | 変数名 | 指定できる値 | 標準値 |
|:---|:----|:-------|:----|
| 編集領域のフォントにアンチエイリアスをかける | uim-xim-use-xft-font? | #t #f  | #f  |
| 編集領域に使用されるフォント名 (アンチエイリアス時) | uim-xim-xft-font-name | "文字列"  | "Sans" |

## FAQ ##

### 候補ウィンドウの表示位置がおかしい ###

On-The-Spotスタイルで入力した場合、候補ウィンドウの位置は左下に固定です。 これはXIMの仕様により、On-The-Spotスタイルでは座標を取得できないためです。

### ホットキーが奪われる ###

アプリにuimと同じホットキー存在する場合、アプリ側にキーを奪われます。

### [uim:xim/uim-xim.1](http://uim.googlecode.com/svn/trunk/xim/uim-xim.1)のオリジナルはどこにある? ###

http://bugs.debian.org/300487