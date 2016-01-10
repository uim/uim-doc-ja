= FAQ =



## ある入力方式が使えない ##

予め使いたい変換エンジンをインストールしてから、uimをコンパイルしましたか？ 例えばuimでAnthyを変換エンジンとして使うには、[uim-anthy](UimAnthy.md)モジュールが必要となります。 このモジュールはAnthyを先にインストールしておかなければコンパイルされません。

入力方式のリストに希望の入力方式は表示されていますか？ [uim-pref](UimPref.md)の「使用可能にする入力方式」を見てください。 もしくは[uim-sh](UimSh.md)を次のように実行して確認してみてください。

```
インストール済みの入力方式のリストを表示
$ uim-sh -e installed-im-list
使用可能になっている入力方式のリストを表示
$ uim-sh -e enabled-im-list
```

[uim-canna](UimCanna.md)であればcannaserver、[uim-sj3](UimSj3.md)であればsj3server、[uim-wnn](UimWnn.md)であればjserverは動いてますか？

```
$ ps aux | grep cannaserver
```

## あるアプリで入力できない ##

[uim-fep](UimFep.md)、[uim-xim](UimXim.md)、[uim.el](UimEl.md)、[uim-gtk](UimGtk.md)、[uim-qt](UimQt.md)といった、各ブリッジはインストールされてますか？ 少なくともコンソールでは[uim-fep](UimFep.md)、Xでは[uim-xim](UimXim.md)が必要です。

```
$ ps aux | grep uim-xim
```

環境変数は正しく指定できていますか？ 正しく指定できていれば次のように表示されるはずです。

```
$ echo $XMODIFIERS
@im=uim
$ echo $GTK_IM_MODULE
uim
$ echo $QT_IM_MODULE
uim
```

期待しているものとは違う入力方式になっていませんか？ [uim-im-switcher](UimImSwitcher.md)や[uim-toolbar](UimToolbar.md)などを起動して、現在の入力方式を確認してみてください。

```
$ uim-toolbar-gtk
```

## uimにキーを奪われる ##

[uim-im-switcher](UimImSwitcher.md)、[uim-toolbar](UimToolbar.md)もしくは「入力方式の正副一時切り換え」の「副入力方式」に「直接入力」を指定。 必要に応じて「直接入力」に切り換える。

入力方式の正副一時切り換えをするためのホットキーは、標準ではMeta+Spaceに割り当てられていますが、[uim-pref](UimPref.md)で好きなキーに変更できます。


## 「くぁｗせｄｒｆｔｇｙふじこｌｐ；＠」が入力できない ##

uim 1.6 から利用可能となった、「ローマ字 - かな変換」設定の「かなに対応しない子音をローマ字として残す」を有効にしてください。

## uim-atokはないの？ ##

今のところありません。 uimの中の人のプライオリティも低目です。 やる気のある外部の人が現われるのを待ちましょう。

## "uim"は何の略ですか ##

Universal Input Methodの略。

http://lists.freedesktop.org/archives/uim/2006-November/001645.html

```
Yes, it is defined as an acronym of "Universal Input Method".
```

昔はuim isn't mockupの略だった。

http://lists.sourceforge.jp/mailman/archives/anthy-dev/2003-August/000199.html

## "uim"ってどう発音するの？ ##

"you ai em"らしい。

http://lists.freedesktop.org/archives/uim/2006-December/001651.html

```
Spell each letters separately as "you ai em", as if it is written as 'UIM'.
```

## "UIM"、"Uim"、"uim"、どれが正しいの？ ##

全部小文字で"u" "i" "m"が正解。

http://lists.freedesktop.org/archives/uim/2006-November/001645.html

```
But 'uim' is the official form as a proper noun.
So please use the all lower-case form even if in a context that 'perl' should be written as 'Perl'.
```

昔は全部大文字で"U" "I" "M"だった。

http://lists.sourceforge.jp/mailman/archives/anthy-dev/2003-August/000195.html

## uim関係のAAはありますか？ ##

依頼:: http://aa5.2ch.net/test/read.cgi/aasaloon/1153392783/123n完成:: http://aa5.2ch.net/test/read.cgi/aasaloon/1153392783/146n

```
.　　　 ／￣ヽ　　　　　 　 　 　 　 　 　 　 　 __
　　 , ′　　 ,′　　,　-ﾍ　　　　　　　 　 　 (_丿
　　,'　　 　 /　 　 /　 　 l　　 /　7　 /　7 /　7/￣'￣ヽ '´￣ヽ
　　! 　 　 /　　　,'　　 　 |　 /　/　 /　/ /　//　/⌒7　/⌒7　}
　　',　　　｀、　_/　　 　 /　/　/　 /　/ /　//　/　 /　/　 /　/
. 　 ヽ　　 /　/　　　　 /　 {　└‐'′/ /　//　/　 /　/　 /　/
　　　 ＼/　/ 　 　 _／　　 ｀ｰ-‐^ｰ' └‐'└‐'　 └‐'　 └‐′
　　　　　　　￣￣´
```

きぐるみギコヴァージョン:: http://utyuuzin.net/d/20060728.html#p02

```
.　　　 ／￣ヽ　　　　　 　 　 　 　 　 　 　 　 __
　　 , ′　　 ,′　　,　-ﾍ　　　　　　　 　 　 (_丿
　　,'　　 　 /　 　 /　 　 l　　 /　7　 /　7 /　7/￣'￣ヽ '´￣ヽ
　　! 　 　 /　　　,'　　 　 |　 /　/　 /　/ /　//　/⌒7　/⌒7　}
　　',　　　｀、　_/　　 　 /　/　/　 /　/ /　//　/　 /　/　 /　/
. 　 ヽ　　 /　/　　　　 /　 {　└‐' (,,ﾟДﾟ)//　/　 /　/　 /　/　＜この先生きのこれるか微妙だぞｺﾞﾙｧ
　　　 ＼/　/ 　 　 _／　　 ｀ｰ-‐^ｰ' └‐'└‐'　 └‐'　 └‐′
　　　　　　　 ￣￣　　　　　　　 　 .U U
```

http://pc8.2ch.net/test/read.cgi/linux/1122652270/197

```
　　 ,: ;;;;;;:
　 ;;;;;;;;;;;;;;: 　　　　　　　　　　　　　　　　 　　;;;;;:
. ;;;;;;;;;;;;;;;;;: 　　　: ;;;;;;;;;:
;;;;;;;;;;;;;;;;;;: 　　　: ;;;;;;;;;;;;;;　　;;;;;: 　　;;;;;;: 　 .;;;;;;:　 .;;;;;;;;;;;;;;;....;;;;;;;;;;;;.
;;;;;;;;;;;;;;;;: 　　　: ;;;;;;;;;;;;;;;: 　:;;;;;: 　 .;;;;;;;: 　 ;;;;;;:　 ;;;;;;: 　;;;;;;:　 . :;;;;;:
;;;;;;;;;;;;;;;;: 　　 .;;;;;;;;;;;;;;;;;;: 　;;;;;;: 　 .;;;;;;;:　 .;;;;;:　 .;;;;;: 　 ;;;;;: 　 . ;;;;;:
: ;;;;;;;;;;;;;;:　:;;;;;;;;;;;;;;;;;;;;;: 　 :;;;;: 　.;;;;;;;;: 　 .;;;;;:　 .;;;;;;:　 .;;;;;: 　 . ;;;;;:
　: ;;;;;;;;;:　:;;;;;;;;;;;;;;;;;;;: . .　 ::;;;;;;;;;;; ;;;;; 　.;;;;;;: 　:;;;;: 　.;;;;;;: 　 . ;;;;:
　　 : : 　;;;;;;;;;;;;;;:
```

ロゴの愛称は'''便座''':: http://pc8.2ch.net/test/read.cgi/linux/1105419571/611n便座:: http://pc8.2ch.net/test/read.cgi/linux/1105419571/897n

```
　　　便座！便座！
　 _ 　∩ 　　　　　,-― ､
(　ﾟ∀ﾟ)彡／／　/　　　` i
　⊂彡　　_...,,＿ |_　 　　i |
　　　　　〈　　　　　＼　　 ,|
　　　　　　＼　　　// ヽ 丿
　　　||l　　　　＞====||l=
　　　　　　／|l 　 　 　/　|" 　　バコタン！
　　　ノ　/､　　 　　 ／/ }
　　　)　 ヽ､＿＿i||,.／　/　 　ベコタン！
　　　 ⌒　,〉　　,,　 　 ",〉
　　　　　 〈　_　_　　, ／
　　　　 　 ｀ー--‐''"
```

## API標準化の件について ##

参加する予定は当面なし。とのこと。

## なぜuimはCで書かれているの？ ##

安定したABIを保証できるから。

## なぜuimはSchemeインタープリタを内蔵しているの？ ##

生産性を高めるため。

## 利用可能な入力方式のリストを得る ##

```
$ uim-sh -e enabled-im-list
```

```
$ uim-fep -h
```

```
$ uim-xim --list
```

## Emacsでuimにキーを奪われる ##

XIMを無効にして、入力を[uim.el](UimEl.md)ブリッジ経由で行なう。

```
$ XMODIFIERS="@im=none" emacs
```

もしくは ~/.Xresourcesや~/.Xdefaultsあたりに

```
Emacs*useXIM: false
```

emacs -nwで起動しているなら、端末自体に指定しましょう。

```
$ XMODIFIERS="@im=none" xterm
```

## VimのLatex-Suiteで入力がおかしくなる ##

http://pc11.2ch.net/test/read.cgi/unix/1151423973/935

```
苦労しましたがなんとか解決しました。
vim7.0で、全てのパッチを当てた後、さらにこちら
http://yukihiro.nakadaira.googlepages.com/
のim patchというのを当ててmakeしたらOKでした。

ただし、そのままではlatex-suiteが自動起動されず、
let g:tex_flavor = "latex"
をする必要がありました。（これはけっこうはまった、、、）

これで、拡張子texのファイルを開くと自動的にlatex-suiteが有効になります。
uimでの入力も正常にできます。(anthyもSKKもOKでした)
```

http://pc11.2ch.net/test/read.cgi/unix/1151423973/943

```
>>935
それたぶん q と . が使えなくなるのでこのコードも追加したほうがいいかもしんないです。
あと完成度はかなり低いんでそのつもりで。ほとんど問題ないとは思いますが。
diff -r b78008b446f1 -r 84cf8763794e src/getchar.c
--- a/src/getchar.c Wed Feb 28 12:47:30 2007 +0900
+++ b/src/getchar.c Sun Mar 04 07:54:34 2007 +0900
@@ -1606,6 +1606,8 @@ vgetc()
     curbuf->b_p_fo = "";
     curbuf->b_p_fex = "";
     ++no_mapping;
+    ++allow_keys;
+    block_redo = TRUE;
     continue;
  }
  else if (c == K_IM_SEQUENCE_END)
@@ -1613,6 +1615,8 @@ vgetc()
     curbuf->b_p_fo = p_fo_save;
     curbuf->b_p_fex = p_fex_save;
     --no_mapping;
+    --allow_keys;
+    block_redo = FALSE;
     continue;
  }
     }
```

## たまに[uim-xim](UimXim.md)が暴走する ##

--asyncオプションを試してみて。

## Flash上での入力問題色々 ##

  * Flash Player（<< 9.0.115）では入力に[uim-xim](UimXim.md)が必要です。
  * Flash Player（>= 9.0.64）とuim（<< 1.3.0）の組み合わせでは、以下のような不具合が発生します。
    1. 編集領域が表示されない
    1. 候補ウィンドウがおかしな位置に出る
  * Flash Player（>= 9.0.115）では、以下のような不具合が発生します。
    1. 編集領域がおかしな位置に出る
    1. 候補ウィンドウがおかしな位置に出る
    1. 特定のロケールで変換確定すると違う文字が入力される
  * windowlessモードで入力できないのはブラウザやFlash Player側の問題です。

## [UimQt](UimQt.md)を使うとQt4アプリが起動できなくなる ##

uim（>= 1.5.3）を使ってください。


## uim-anthyのF10がGTKアプリに取られて半角英数変換できない ##

http://vagus.seesaa.net/article/108510198.html

  * gconf-editor の apps -> metacity -> window\_keybindings -> activate\_window\_menu を F10 から disabled などに変更する
