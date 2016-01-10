= uim-fep =



## これは何？ ##

uimとコンソールのブリッジ。 コンソールで入力を行なう場合に使う。

詳しくは[uim-fep wiki](http://www.ice.nuie.nagoya-u.ac.jp/~h013177b/uim-fep/)を参考に。

## 使い方 ##

LANGに使用する言語とエンコーディングを設定します。 LC\_ALLかLC\_CTYPEでもいいです。 サポートされている言語とエンコーディングは

```
locale -a
```

で確認できると思います。

```
例 sh系でja_JP.EUC-JPにする
$ LANG=ja_JP.EUC-JP ; export LANG

例 csh系でja_JP.UTF-8にする
% setenv LANG ja_JP.UTF-8

例 SolarisでEUC-JPで使う
$ LANG=ja ; export LANG
% setenv LANG ja
```

```
$ uim-fep
```

SHELLが起動します。

標準の入力方式は[UimPref](UimPref.md)で設定できます。 または~/.uimに

```
(define default-im-name 'anthy)
```

のように書きます。

### リダイレクトの動作 ###

標準出力のリダイレクトはuim-fepと子プロセス（シェル）のすべての出力を変更します。

```
例: logにすべての出力を書き込む（scriptコマンドと同じ）
$ uim-fep | tee log
```

入力のリダイレクトは子プロセスの標準入力を変更します。

```
例: lsの出力をw3mで見る
$ ls | uim-fep -e w3m
```

### termcap/terminfo ###

uim-fepではtermcap/terminfoを使って端末の情報を取得します。 以下のエントリを使用してカーソルの位置や文字の属性を変えます。

#### ほとんどの端末の場合 ####



&lt;esc&gt;

[6nでカーソル位置が取得できる端末では以下のエントリを使用します。

| terminfo | termcap | 意味 |
|:---------|:--------|:---|
| smul     | us      | アンダーライン開始 |
| rmul     | ue      | アンダーライン終了 |
| smso     | so      | 強調開始 |
| rmso     | se      | 強調終了 |
| sgr0     | me      | 全ての文字属性を終了 |
| cup      | cm      | カーソルを指定した位置に移動 |

以下のエントリは最下行をステータスラインとして使うときだけ必要になります。

| terminfo | termcap | 意味 |
|:---------|:--------|:---|
| el       | ce      | 行末まで削除 |
| csr      | cs      | スクロール領域を変更 |
| clear    | cl      | 画面を消去 |
| ed       | cd      | カーソル位置から画面の最後まで消去 |

以下のエントリは-oオプションを指定した場合に使用されます。

| terminfo | termcap | 意味 |
|:---------|:--------|:---|
| ich      | IC      |
| dch      | DC      |

#### DOSプロンプト等 ####

DOSプロンプトのような

&lt;esc&gt;

[6nでカーソル位置が取得できない端末では以下のエントリが必要になります。

| terminfo | termcap | 意味 |
|:---------|:--------|:---|
| smul     | us      | アンダーライン開始 |
| rmul     | ue      | アンダーライン終了 |
| smso     | so      | 強調開始 |
| rmso     | se      | 強調終了 |
| sgr0     | me      | 全ての文字属性を終了 |
| sc       | sc      | カーソル位置を保存 |
| rc       | rc      | カーソル位置を復元 |
| cub1     | le      | カーソルを左に移動 |
| cuf1     | nd      | カーソルを右に移動 |

以下のエントリは最下行をステータスラインとして使うときだけ必要になります。

| terminfo | termcap | 意味 |
|:---------|:--------|:---|
| el       | ce      | 行末まで削除 |
| csr      | cs      | スクロール領域を変更 |
| clear    | cl      | 画面を消去 |
| ed       | cd      | カーソル位置から画面の最後まで消去 |
| cup      | cm      | カーソルを指定した位置に移動 |
| cuu1     | up      | カーソルを上に移動 |

以下のエントリは-oオプションを指定した場合に使用されます。

| terminfo | termcap | 意味 |
|:---------|:--------|:---|
| ich      | IC      |
| dch      | DC      |

#### キーを識別するために必要なエントリ ####

以下のエントリを利用して、押下されたキーが何であるかを判断します。

| kbs | kb | backspaceキー |
|:----|:---|:------------|
| kdch1 | kD | deleteキー    |
| kcub1 | kl | ←キー         |
| kcuu1 | ku | ↑キー         |
| kcur1 | kr | →キー         |
| kcud1 | kd | ↓キー         |
| kpp | kP | Page Upキー   |
| knp | kN | Page Downキー |
| khome | kh | Homeキー      |
| kend | @7 | Endキー       |
| kich1 | kI | Insertキー    |
| kf1 | k1 | F1キー        |
| kf2 | k2 | F2キー        |
| kf3 | k3 | F3キー        |
| kf4 | k4 | F4キー        |
| kf5 | k5 | F5キー        |
| kf6 | k6 | F6キー        |
| kf7 | k7 | F7キー        |
| kf8 | k8 | F8キー        |
| kf9 | k9 | F9キー        |
| kf10 | k; | F10キー       |
| kf11 | F1 | F11キー       |
| kf12 | F2 | F12キー       |

どの端末のエントリを使うかは環境変数TERMで決まるのでTERMを使用している 端末に合うように設定してください。

#### 端末の機能のメモ ####

  * mlterm (2.7.0)
    * save\_cursor(sc)でカーソルの位置しか保存されない。
    * 一回のsave\_cursor(sc)にたいして一回のrestore\_cursor(rc)しかできない。
    * cursor\_left(cub1)で右端から次の行の左端に移動できない。
    * cursor\_right(cuf1)で左端から前の行の右端に移動できない。
    * 全角文字も1回のdelete\_character(dch1)で消える。
    * cursor\_invisible(civis)でカーソルが消えない。
    * termcap/terminfoのexit\_standout\_mode(rmso), exit\_underline\_mode(rmul)はexit\_attribute\_mode(sgr0)と同じになっている。
  * jfbterm (0.4.6)
    * save\_cursor(sc)でカーソルの位置、色、属性が保存される。
    * save\_cursor(sc)した回数だけrestore\_cursor(rc)が使える。(スタック)
    * cursor\_left(cub1)で右端から次の行の左端に移動できない。
    * cursor\_right(cuf1)で左端から前の行の右端に移動できない。
    * cursor\_invisible(civis)でカーソルが消えない。
  * kon
    * save\_cursor(sc)でカーソルの位置、色、属性が保存される。
    * 一回のsave\_cursorにたいして一回のrestore\_cursor(rc)しかできない。
    * cursor\_left(cub1)で右端から次の行の左端に移動できない。
    * key\_left(kcub1)で右端から次の行の左端に移動できる。
    * cursor\_right(cuf1)で左端から前の行の右端に移動できる。
    * cursor\_invisible(civis)でカーソルが消える。
  * screen (4.0.2)
    * save\_cursorで位置、色，属性が保存される。
    * save\_cursor(sc)は1つしか保存できないが、restore\_cursor(rc)で何回も復元できる。
    * cursor\_left(cub1)で右端から次の行の左端に移動できる。
    * cursor\_right(cuf1)で左端から前の行の右端に移動できない。
  * rxvt (2.7.10)
    * enter\_ca\_mode(smcup)の後にrestore\_cursor(rc)ができなくなる。

### オプション ###

-u ''入力方式名'':: 入力方式を指定します。-s {'''lastline''','''backtick''','''none'''}:: ステータスラインの表示場所を指定します。'''-sl'''、'''-sb'''、'''-sn'''のように省略できます。-b ''ファイル名'':: backtickで使うsocketのパスを指定します。相対パスのときは、環境変数'''TMP'''か/tmpからのパスになります。-w ''数値'':: ステータスラインの幅です。-t ''秒'':: rshを使っていると"F1"、"up"、"

&lt;Alt&gt;

a"などが認識されないことがあります。これはエスケープシーケンスが一度に入力されないからです。そのような場合はこのオプションでエスケープのあとの待ち時間を設定します。このオプションを付けないときの待ち時間は0秒です。

```
例 待ち時間を0.1秒にする
$ uim-fep -t 0.1
```

-C ''前景色:: 背景色'':編集領域や'''-s lastline'''のときのステータスラインの色を指定します。使用するアプリケーションの背景色が通常の背景色と違う場合にこのオプションで色を合わせてください。''前景色''、''背景色''の部分は次の16色が使えます。'''lightblack'''より下の色は表示できない端末があります。

|  | 省略記法 |
|:-|:-----|
| black | k    |
| red | r    |
| green | g    |
| yellow | y    |
| blue | b    |
| magenta | m    |
| cyan | c    |
| white | w    |
| lightblack | lk   |
| lightred | lr   |
| lightgreen | lg   |
| lightyellow | ly   |
| lightblue | lb   |
| lightmagenta | lm   |
| lightcyan | lc   |
| lightwhite | lw   |

```
例 前景色を白、背景色を黒にしてjedを起動する
$ uim-fep -C white:black -e jed
例 背景色を青にする
$ uim-fep -C :blue
例 前景色を黄色にする
$ uim-fep -C yellow:
```

-c:: カーソル位置の文字を反転表示します。kterm、aterm、rxvt、teraterm（カーソル点滅なしの状態）などの端末では反転された文字にカーソルがあると反転が消えることがあります。このような場合はこのオプションを付けると反転文字にカーソルがあるときに反転されるようになります。-i:: ステータスラインを描画しているときや編集領域の末尾以外を編集しているときにカーソルを一時的に消します。カーソルの残像が気になるときはこのオプションを付けてください。-o:: 編集領域の表示スタイルをOn-The-Spotにします。jedなどの背景色があるアプリケーションを使うと右端の背景色が消えることがあります。-S:: GNU screenでフィルタとして使えるようにします。（GNU screen 4.0.2以降）例えば、~/.screenrcに

```
bind J exec | uim-fep -S
bind K eval 'exec cat' kill redisplay
```

このように書けば、Ctrl+a Jでuim-fepをフィルタとして起動し、Ctrl+a Kで終了できるようになります。'''-s'''オプションにかかわらずモード表示にはbacktickが使われます。'''UIM\_FEP\_SETMODE'''、'''UIM\_FEP\_GETMODE'''の値は$HOME/.uim.d/fep/setmode-$STY-$WINDOW-screen、$HOME/.uim.d/fep/getmode-$STY-$WINDOW-screenになります。

-f ''str'':: $UIM\_FEP\_SETMODEと$UIM\_FEP\_GETMODEのファイル名をuim-fep-setmode-{str}、uim-fep-setmode-{str}にします。{str}は'''-f'''オプションの引数です。'''UIM\_FEP\_SETMODE'''と'''UIM\_FEP\_GETMODE'''が置かれるディレクトリは$HOME/.uim.d/fep/です。-d:: 候補一覧の表示スタイルをddskkのようにします。-K:: 押されたキーの~/.uimでの表記を示します。'''-t'''オプション以外のオプションは無視されます。-e ''command arg1 arg2 ...'':: 起動するコマンドを指定します。このオプション以降の引数は''command''に渡されます。-h:: ヘルプメッセージを表示します。-v:: バージョンを表示します。

### ファイル ###

~/.uim.d/fep/getmode-$UIM\_FEP\_PID:: uim-fepのモードが書き込まれるファイル~/.uim.d/fep/setmode-$UIM\_FEP\_PID:: このファイルにモードを書き込むとuim-fepのモードが変わる

### 環境変数 ###

UIM\_FEP\_PID

UIM\_FEP\_GETMODE

UIM\_FEP\_SETMODE

## backtickの使い方 ##

GNU screen 3.9.15以降が必要です。

uim-fep-tickをパスの通ったところに置いてください。 ~/.screenrcに

```
backtick 0 0 0 uim-fep-tick
hardstatus alwayslastline "%0`"
```

と書きます。

screenのウィンドウで

```
$ uim-fep -s backtick
```

と起動します。

uim-fepはscreen内の複数のウィンドウで起動できます。

uim-fep-tickはscreenから起動されるため、screenの環境変数が引き継がれます。

backtickの反応がなくなったら

```
$ screen -X backtick 0 0 0 uim-fep-tick
```

と起動してください。

### screen-uimのように使う ###

(screen 4.0.2以降) uim-fepはscreen-uimのようにscreen内でフィルタとして使うことができます。 あらかじめuim-fepを起動しておく必要がなく、起動したいときにすぐ起動できるのが便利です。

設定は~/.screenrcに

```
backtick 0 0 0 uim-fep-tick
hardstatus alwayslastline "%0`"
bind j exec | uim-fep -S
bind k eval 'exec cat' kill redisplay
```

このように書きます。 これで、C-a jでuim-fepが起動します。 モードはbacktickに表示されます。 終了はC-a kです。

フィルタは2つ起動できないので、uim-fepが起動しているときは他のフィルタは起動できません。 ですが、フィルタとして使っていないexecはbacktick 9 0 0で代用できます。 execの場合は起動されるプロセスにWINDOWとSTYの環境変数が設定されますが、backtickの場合はこれらの環境変数は設定されません。

### uim-fep-tickのオプション ###

-s ''ファイル名'':: socketのパスを指定できます。相対パスのときは、$HOME/.uim.d/fep/からのパスになります。-h:: ヘルプメッセージを表示します。-v:: バージョンを表示します。

### uim-fep-tickのファイル ###

~/.uim.d/fep/getmode-$UIM\_FEP\_PID-$WINDOW-screen:: uim-fep-tickのモードが書き込まれるファイル。~/.uim.d/fep/setmode-$UIM\_FEP\_PID-$WINDOW-screen:: このファイルにモードを書き込むとuim-fep-tickのモードが変わる。

## 問題点 ##

### 表示の乱れ ###

編集領域の編集中に端末のサイズが変更されると表示が乱れることがあります。

### 暴走 ###

screenの中でuim-fepを'''-s lastline'''で使っているとき端末のサイズを変更すると稀にscreenが暴走することがあります。

無反応になったり暴走したりしたら

```
$ kill -INT <uim-fepのpid>
```

このコマンドで直ると思います。 ただし変換はできなくなります。

## 注意 ##

### ペースト ###

中ボタンクリックやShift+Insertのペーストなどで一度に大量に入力されたときは変換せずにそのまま出力されます。 プリエディットを入力中にペーストすると無効になります。

端末の右端でプリエディットを開始すると次の行に移ります。

### キー ###

Altキーを使うにはAltを押しながら他のキーを押したときに、^[が出力されるようにします。 mltermの場合は~/.mlterm/mainに次のように書きます。

```
mod_meta_mode=esc
```

ktermの場合は~/.Xresourceか~/.Xdefaultsに次のように書きます。

```
KTerm*EightBitInput: false
```

uim-fepはコンソールにおける制約をそのまま受けるため、標準のキー設定では以下の事ができません。

  * [UimAnthy](UimAnthy.md)、[UimCanna](UimCanna.md)、[UimMana](UimMana.md)、[UimWnn](UimWnn.md)、[UimSj3](UimSj3.md)
    * オン/オフができない（Shift+Space、全角/半角）
    * 入力モードの推移ができない（Shift+F{6,7,8,9,10}）
    * 文節を縮められない（Shift+←、Ctrl+i）
  * [UimByeoru](UimByeoru.md)
    * オン/オフができない（Shift+Space）
  * [UimLook](UimLook.md)
    * オン/オフができない（Shift+Space、全角/半角）
  * [UimPrime](UimPrime.md)
    * 全角英数入力モードへ移行できない（Ctrl+L）

この問題を回避するには、[UimPref](UimPref.md)などで適当なキーを追加してください。 uim-fepが利用可能なキーは、付属の[uim:fep/README.key](http://uim.googlecode.com/svn/trunk/fep/README.key)に書かれています。 例外としてCtrl+iと共にTabキーを追加することで、Ctrl+iも使えるようになります。

Alt+F1、Alt+→などが使える端末もあります。

## 仕様 ##

uim-fep -e screenで起動して入力した後、しばらく放置するカーソルが勝手に編集領域の先頭へ移動する。
