= uim-toolbar =

## これは何？ ##

使用中の入力方式のモード表示/切り換えや各種ツールを起動するバー。 右クリックメニューから、各種ツールを起動する事ができます。

  * スタンドアローンタイプ
    * uim-toolbar-gtk
    * uim-toolbar-qt
    * uim-toolbar-qt4
  * システムトレイタイプ
    * uim-toolbar-gtk-systray
  * パネルアプレットタイプ
    * uim-applet-gnome
    * uim-applet-kde
    * uim-applet-kde4

なおuim-toolbar-qt、uim-applet-kde、uim-toolbar-qt4とuim-applet-kde4は標準では含まれません。uim-toolbar-qtとuim-applet-kdeは'''--with-qt'''、uim-toolbar-qt4とuim-applet-kde4は'''--with-qt4'''をつけてuimをコンパイルする必要があります。

## 使い方 ##

スタンドアローンタイプはターミナルエミュレータなどからuim-toolbar-gtk、uim-toolbar-qtもしくはuim-toolbar-qt4を起動します。

```
$ uim-toolbar-gtk &
```

起動中のツールバー左端をダブルクリックすると畳めます（1.3.0以降）。

起動位置を指定したい場合は以下のようにする。

```
$ uim-toolbar-gtk +20+20 &
```

```
$ uim-toolbar-qt -geometry +20+20 &
```

Qt4版 (uim-toolbar-qt4) はuim 1.7.0から指定できるようになりました。
```
$ uim-toolbar-qt4 -geometry +20+20 &
```

システムトレイタイプはシステムトレイが存在する状態でuim-toolbar-gtk-systrayを起動します。

```
$ uim-toolbar-gtk-systray &
```

パネルアプレットタイプは、GNOME/KDEパネルなどにアプレットの1つとして追加して使います。 アプレットはパネルの右クリックメニューなどから追加できます。

### 手書き入力パッドボタン ###

[uim-tomoe-gtk](http://sourceforge.net/projects/tomoe/)を別途インストールする必要があります。

### ヘルプボタン ###

wikiページを参照します。

### ファイル ###

~/.uim.d/customs/custom-toolbar.scm:: [UimPref](UimPref.md)の「ツールバー」ファイル。

## カスタマイズ可能な項目 ##

### ツールバーの変数 ###

| 動作 | 変数名 | 指定できる値 | 標準値 |
|:---|:----|:-------|:----|
| 入力方式切り換えメニューを有効にする | toolbar-show-action-based-switcher-button? | #t #f  | #t  |
| 変更の適用範囲 | imsw-coverage | 'focused-context<br> 'app-global<br> 'system-global <table><thead><th> 'system-global </th></thead><tbody>
<tr><td> フル機能の入力方式切り換えツール </td><td> toolbar-show-switcher-button? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> 設定 </td><td> toolbar-show-pref-button? </td><td> #t #f  </td><td> #t  </td></tr>
<tr><td> 日本語辞書ツール </td><td> toolbar-show-dict-button? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> 入力パッド </td><td> toolbar-show-input-pad-button? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> 手書き入力パッド </td><td> toolbar-show-handwriting-input-pad-button? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> ヘルプ </td><td> toolbar-show-help-button? </td><td> #t #f  </td><td> #f  </td></tr></tbody></table>

<h4>ツールバーの変数の依存関係</h4>

<ul><li>toolbar-show-action-based-switcher-button? #f<br>
<ul><li>imsw-coverage</li></ul></li></ul>

<h2>既知のバグ</h2>

<h3>システムトレイ版で各ボタンの幅が狭くなる</h3>

多くのシステムトレイは、アイテム1つに対してアイコン1つという仕様になっていますが、uimではアイテム1つに対して複数のアイコンを詰め込んでいるためです。<br>
<br>
<ul><li><a href='http://lists.sourceforge.jp/mailman/archives/anthy-dev/2005-January/001640.html'>http://lists.sourceforge.jp/mailman/archives/anthy-dev/2005-January/001640.html</a>
</li><li><a href='http://garakuta.homelinux.org/~nosuke/diary/diary.html?y=2006&m=8&d=29&n=1#29-1'>http://garakuta.homelinux.org/~nosuke/diary/diary.html?y=2006&amp;m=8&amp;d=29&amp;n=1#29-1</a>
</li><li><a href='http://bugs.debian.org/400880'>http://bugs.debian.org/400880</a></li></ul>

<h3>起動するアプリを変更できない</h3>

現在のところハードコードされているので、変更するにはソースコードを直接編集する必要があります。<br>
<br>
<ul><li><a href='http://uim.googlecode.com/svn/trunk/helper/toolbar-common-gtk.c'>uim:helper/toolbar-common-gtk.c</a>
</li><li><a href='http://uim.googlecode.com/svn/trunk/qt/toolbar-common-quimhelpertoolbar.cpp'>uim:qt/toolbar-common-quimhelpertoolbar.cpp</a>
</li><li><a href='http://uim.googlecode.com/svn/trunk/qt4/toolbar/common-quimhelpertoolbar.cpp'>uim:qt4/toolbar/common-quimhelpertoolbar.cpp</a></li></ul>

<h3>トレイの高さが32px以下だとアイコンが全部表示されない</h3>

仕様?