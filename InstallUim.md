= インストール =



## uimの入手 (ソースコードを利用) ##

### リリース版 ###

ソースコードをhttp://code.google.com/p/uim/downloads/list
からダウンロードしてきます。 これにはコアライブラリ、各種モジュール、ブリッジ、ツール群、アイコンやドキュメントなど一式が同梱されています。

ソースコードをダウンロードしてきたら展開しましょう。

```
$ tar xvzf uim-x.x.x.tar.gz
```

展開したら、uimのソースツリーのトップレベルに移動して、configureスクリプトを実行します。

```
$ cd uim-x.x.x
$ ./configure
```

以下は標準で無効になっているので、必要であれば明示的に指定してください。

  * --enable-debug（デバッグ情報を埋め込む）
  * --enable-backtrace（Backtraceを出力する）
  * --enable-dict（[UimDictGtk](UimDictGtk.md)のビルド）
  * --enable-anthy-static（[UimAnthy](UimAnthy.md)のスタティックビルド）
  * --enable-anthy-utf8-static（UTF-8版[UimAnthy](UimAnthy.md)のスタティックビルド）
  * --enable-kde4-applet (KDE4 向けアプレットのビルド)
  * --with-anthy-utf8（UTF-8版[UimAnthy](UimAnthy.md)をビルド）
  * --with-canna（[UimCanna](UimCanna.md)のビルド）
  * --with-sj3（[UimSj3](UimSj3.md)のビルド）
  * --with-wnn（[UimWnn](UimWnn.md)のビルド）
  * --with-scim（uim-scimのビルド, broken）
  * --with-qt（各種Qt3.x版ツールのビルド）
  * --with-qt-immodule（Qt 3.x版[UimQt](UimQt.md)のビルド）
  * --with-qt4（各種Qt4.x版ツールのビルド）
  * --with-qt4-immodule（Qt 4.x版[UimQt](UimQt.md)のビルド）
  * --with-eb（電子辞書を利用した注釈表示）
  * --with-curl (cURLプラグインのビルド)
  * --with-expat (expatプラグインのビルド, uim-yahoo-jp に必要)
  * --with-sqlite3 (SQLite3プラグインのビルド)
  * --with-ffi (libffiプラグインのビルド)

各ブリッジ、モジュール、ツール群をビルドするために、以下が要求されます。

  * iconv
  * [gettext](http://www.gnu.org/software/gettext/)（>= 0.17）
  * [pkg-config](http://pkgconfig.freedesktop.org/)
  * [Anthy](http://anthy.sourceforge.jp/)（>= 7802 推奨）
    * [UimAnthy](UimAnthy.md)
    * [UimDictGtk](UimDictGtk.md)のAnthy個人辞書サポート
  * [Canna](http://canna.sourceforge.jp/)
    * [UimCanna](UimCanna.md)
    * [UimDictGtk](UimDictGtk.md)のCanna個人辞書サポート
  * [Mana](http://sourceforge.jp/projects/shinji/)（>= 0.2.0 推奨）
    * [UimMana](UimMana.md)
  * [PRIME](http://taiyaki.org/prime/)（>= 0.8.5.2）
    * [UimPrime](UimPrime.md)
  * [m17n](http://www.m17n.org/m17n-lib-ja/)（>= 1.3.1）
    * uim-m17nlib
  * curses
    * [UimFep](UimFep.md)
    * [UimSh](UimSh.md)
  * X11
    * [UimXim](UimXim.md)
  * [GTK+](http://www.gtk.org/)（>= 2.4）
    * [UimGtk](UimGtk.md)
    * uim-toolbar-gtk（[UimToolbar](UimToolbar.md)）
    * uim-toolbar-gtk-systray（[UimToolbar](UimToolbar.md)）
    * uim-pref-gtk（[UimPref](UimPref.md)）
    * [UimInputPadJa](UimInputPadJa.md)
    * [UimDictGtk](UimDictGtk.md)
    * uim-candwin-gtk（[UimXim](UimXim.md)）
  * [GTK+](http://www.gtk.org/)（>= 3）
    * uim-gtk3 ([UimGtk](UimGtk.md))
    * uim-toolbar-gtk3（[UimToolbar](UimToolbar.md)）
    * uim-toolbar-gtk3-systray（[UimToolbar](UimToolbar.md)）
    * uim-pref-gtk3（[UimPref](UimPref.md)）
    * uim-input-pad-ja-gtk3 ([UimInputPadJa](UimInputPadJa.md))
    * uim-dict-gtk3 ([UimDictGtk](UimDictGtk.md))
    * uim-candwin-gtk3（[UimXim](UimXim.md)）
  * [gnome-panel-2](http://www.gnome.org/)、[intltool](ftp://ftp.gnome.org/pub/GNOME/sources/intltool/)（>= 0.36.3）
    * uim-applet-gnome（[UimToolbar](UimToolbar.md)）
  * [gnome-panel-4](http://www.gnome.org/)
    * uim-applet-gnome3（[UimToolbar](UimToolbar.md)）
  * [Qt](http://www.trolltech.com/products/qt)（>= 3.3.2, << 4.0）
    * uim-toolbar-qt（[UimToolbar](UimToolbar.md)）
    * uim-pref-qt（[UimPref](UimPref.md)）
    * [UimChardictQt](UimChardictQt.md)
    * uim-candwin-qt（[UimXim](UimXim.md)）
  * immodule for Qtのパッチ]を当てたQt
    * Qt 3.x版[UimQt](UimQt.md)
  * [Qt](http://www.trolltech.com/products/qt)（>= 4.0）
    * uim-toolbar-qt4（[UimToolbar](UimToolbar.md)）
    * uim-pref-qt4（[UimPref](UimPref.md)）
    * uim-chardict-qt4（[UimChardictQt](UimChardictQt.md)）
    * uim-candwin-qt4（[UimXim](UimXim.md)）
    * Qt 4.x版[UimQt](UimQt.md)
  * [kdelibs](http://www.kde.org/)（<< 4.0）
    * uim-applet-kde（[UimToolbar](UimToolbar.md)）
    * knotify3状態通知
  * [kdelibs](http://www.kde.org/)（>= 4.2）
    * uim-applet-kde4（[UimToolbar](UimToolbar.md)）
  * [CMake](http://cmake.org/)
    * uim-applet-kde4（[UimToolbar](UimToolbar.md)）
  * [libedit](http://www.thrysoee.dk/editline/)
    * [UimSh](UimSh.md)の行編集、コマンド履歴サポート（uim-editline）
  * [libnotify](http://www.galago-project.org/news/index.php)（>= 0.4）
    * libnotify状態通知
  * [EB](http://www.sra.co.jp/people/m-kasahr/eb/)
    * 電子辞書を利用した注釈表示

configureスクリプトを正常に実行できたら、makeでコンパイルを行います。

```
$ make
```

makeが終わったら、make installしましょう。

```
$ sudo make install
```

標準では/usr/local以下にインストールされますが、このディレクトリにあるライブラリは標準では検索されません。 /etc/ld.so.confに''/usr/local/lib''という行を追加して、ldconfigを実行する必要があります。

[UimGtk](UimGtk.md)を利用するには、GTK+2 の gtk.immodules
ファイルが正しく生成されている必要があります。

もし GTK+2 と異なるディレクトリにuimをインストールした場合は、明示的に
gtk.immodules ファイルを指定してください。

```
$ export GTK_IM_MODULE_FILE=$(DESTDIR)$(sysconfdir)/gtk-2.0/gtk.immodules
```

### 開発途中版 ###

リリース版では生ぬるい、もっと新しいuimが使いたい、というチャレンジャー な方は、開発途中版のuimを入手できます。 たまにコンパイルが通らなかったりすることがあるかもしれませんけれど。

[Git](http://git-scm.com/)がインストールされているなら

```
$ git clone https://github.com/uim/uim.git
```

で完了です。 同期させるなら、uimのソースツリーのトップレベルディレクトリで

```
$ git pull
```

とするだけでOKです。

uimのソースツリーを取得したら、ソースツリーのトップレベルディレクトリに移動して、make-wc.shスクリプトを実行してください。

```
$ cd uim
$ LC_MESSAGES=C ./make-wc.sh
```

実行するには以下が必要です。

  * [Autoconf](http://www.gnu.org/software/autoconf/)（>= 2.60b（2.61推奨））
  * [Automake](http://www.gnu.org/software/automake/)（>= 1.10）
  * [Libtool](http://www.gnu.org/software/libtool/)（>= 1.5.22）
  * [intltool](http://ftp.gnome.org/pub/GNOME/sources/intltool/)（>= 0.36.3）
  * [GNU make](http://www.gnu.org/software/make/)
  * [Perl](http://www.perl.org/)
  * [Ruby](http://www.ruby-lang.org/)
  * [librsvg](http://librsvg.sourceforge.net/)
  * [AsciiDoc](http://www.methods.co.nz/asciidoc/)
  * ed

ビルドオプションも同時に指定できます。

```
$ LC_MESSAGES=C ./make-wc.sh --enable-debug --enable-backtrace
```

後の作業はリリース版と同じです。 makeでコンパイルしてください。

### Notes for Packagers and System Integrators ###

  * The option "--enable-debug" and/or "--enable-backtrace" makes uim (in accurately, underlying [SigScheme](http://code.google.com/p/sigscheme/) interpreter) quite heavy. Please keep them unspecified for normal library
  * Use the bundled [SigScheme](http://code.google.com/p/sigscheme/), and do not depend on external [SigScheme](http://code.google.com/p/sigscheme/) package. Since the [SigScheme](http://code.google.com/p/sigscheme/) interpreter is completely embedded into libuim without linking to libsscm, and exposing no [SigScheme](http://code.google.com/p/sigscheme/)-specific symbols regardless of environment-dependent symbol exportation control existence such as -export-symbols of libtool or version script of ld, no conflict with libsscm occurs
  * libuim links to libgcroots although [SigScheme](http://code.google.com/p/sigscheme/) is embedded into libuim. Although libgcroots is also bundled in uim, it should be managed as a separated package since both libsscm and libuim which provided by separated package depends on it. Add '--with-libgcroots=installed' to configure options for uim to disable build and install of the bundled version of libgcroots
  * For uim-m17nlib, the command 'uim-m17nlib-relink-icons' to import icons from m17n-db is provided. Run it when m17n-db has been updated. Whether making the command itself available for users or just use it as post-package-install script is the system integrator's choice

一般ユーザに対しては「uimのtarballをダウンロードして configure && makeするだけ」という方針を守っており、必要な物は全て同梱されています。また、パッケージからインストールする場合でも"install uim-anthy"のような指示だけで適切な依存解決や選択肢の提示が行われる事を期待しています。

パッケージャの方々には、申し訳ないですが全ての依存関係を理解してもらうしかありません。本来なら包括的な解説をあらかじめ用意しておくべきですが、後回しにしてしまっています。すいません。不明点は随時質問して下さい。なるべく箇条書きでyes/noで答えられるような形式だと有難いです。

## uimの設定 ##

### Xの起動スクリプトへの追加 ###

環境に合わせて~/.xsessionや~/.xinitrc、~/.gnomerc、~/.xprofileあたりに

```
GTK_IM_MODULE=uim ; export GTK_IM_MODULE
QT_IM_MODULE=uim ; export QT_IM_MODULE
uim-xim &
XMODIFIERS=@im=uim ; export XMODIFIERS
```

を追加してください。

### Emacs/XEmacsの設定ファイルへの追加 ###

環境に合わせて~/.emacsや~/.xemacs/init.elあたりに

```
(require 'uim)
(global-set-key "\C-o" 'uim-mode)
```

を追加してください。 この例ではCtrl+oで[UimEl](UimEl.md)ブリッジが起動します。

### 標準の入力方式を指定 ###

[UimPref](UimPref.md)で設定できます。

```
$ uim-pref-gtk（もしくはuim-pref-{qt,qt4}）
```

  1. 起動したら、「全体設定」→「入力方式の利用準備」→「標準の入力方式を指定」のチェックボックスにチェックを入れます。
  1. そのすぐ下の「標準の入力方式」に、希望の入力方式をセットしてください。
  1. もし「標準の入力方式」の中に、希望の入力方式が見つからなければ、更にその下の「使用可能にする入力方式」の「編集...」ボタンを押して、左の有効アイテムに希望の入力方式を追加してください。
  1. そこにも希望する入力方式が見つからない場合、その入力方式はインストールされていないのかもしれません。確認してみてください。

標準の入力方式を指定していない場合、システムのロケールに従った入力方式を選択されます。 例えば日本語ロケール（ja\_JP）であれば、日本語関係の入力方式が自動で選択されます。

## OS別のインストール例 (パッケージを利用) ##

### Arch ###

Extraに[公式パッケージ](http://www.archlinux.org/packages/extra/i686/uim/)があるようです。

  * http://wiki.archlinux.org/index.php/Input_Japanese_using_UIM_(English)

### CentOS ###

[Karan.Org](http://centos.karan.org/)にあるようですが、詳細不明。

### Debian ###

Okabeさんにより[公式パッケージ](http://packages.qa.debian.org/u/uim.html)が提供されています。 アーカイブが細かく分割されているので、インストールし忘れには注意しましょう。

  * uim
  * uim-common
  * uim-utils
  * libuim-data
  * libuim6
  * libuim6-dbg
  * libuim-dev
  * uim-gtk2.0
  * uim-qt
  * uim-qt3
  * uim-xim
  * uim-fep
  * uim-el
  * uim-anthy
  * uim-byeoru
  * uim-canna
  * uim-hangul
  * uim-ipa-x-sampa
  * uim-latin
  * uim-m17nlib
  * uim-pinyin
  * uim-prime
  * uim-skk
  * uim-tcode
  * uim-viqr
  * uim-applet-gnome
  * uim-applet-kde

とりあえずはuimダミーパッケージを利用するとよいでしょう。

インストールするには

```
# aptitude install uim uim-anthy
```

を実行してください。

設定はim-switchが自動で行います。

  * [Debian GNU/Linux スレッドテンプレ 日本語関係](http://debian.fam.cx/index.php?Japanese)

### Fedora ###

[公式パッケージ](https://admin.fedoraproject.org/pkgdb/acls/name/uim)が提供されています。 アーカイブがが細かく分割されているので、インストールし忘れには注意しましょう。

  * uim
  * uim-devel
  * uim-anthy
  * uim-canna
  * uim-skk
  * uim-m17n
  * uim-gtk2
  * uim-qt
  * uim-qt3
  * uim-qt-common
  * emacs-uim
  * emacs-common-uim
  * xemacs-uim
  * uim-gnome

インストールするには

```
# yum install 'uim*'
```

を実行してください。

im-chooserを利用してuimに切り替えます。

### FreeBSD ###

[Ports](http://www.freebsd.org/cgi/cvsweb.cgi/ports/textproc/uim/)に入っています。

portsupgradeを導入しているなら

```
# portinstall textproc/uim
```

とするとインストールされます。

依存関係でm17n-libがインストールされます。 Options for m17n-libでAnthy supportとIspell supportが選択できます。

uim-skkを利用したい場合，skk-jisyoをインストールします。

```
# portinstall japanese/skk-jisyo
```

### Gentoo ###

Portageで[ebuild](http://www.gentoo-portage.com/app-i18n/uim)が提供されています。

```
# emerge anthy uim
```

とするとインストールされます。

注意点は、[UimAnthy](UimAnthy.md)等を使う時は先にAnthy等を先にemergeしてください。 後からemergeしても使えません。

またインストール前には、各USEフラグを確認してください。 例えば[UimAnthy](UimAnthy.md)を使うならanthy USEフラグを設定しておく必要があります。

[UimXim](UimXim.md)をアンチエイリアスなしで使う場合、jis-fixed-**-jisx0208.1983-0のフォントをインストールしてください。 Xを普通にインストールしただけでは入らないようです（[Anthy-dev 3440](http://lists.sourceforge.jp/mailman/archives/anthy-dev/2007-March/003439.html)）。**

後は環境に合わせて~/.xsessionや~/.xinitrc、~/.gnomerc、~/.xprofileあたりに

```
GTK_IM_MODULE=uim ; export GTK_IM_MODULE
QT_IM_MODULE=uim ; export QT_IM_MODULE
uim-xim &
XMODIFIERS=@im=uim ; export XMODIFIERS
```

を追加してください。

  * GentooJP Wiki 日本語入力設定事例集/uim+anthy

### Mac OS X ###

  * Fink:: http://pdb.finkproject.org/pdb/package.php/uim
  * [MacPorts](http://www.macports.org/):: http://lapangan.net/darwinports/index.php?PrivatePortfile%2Fuim
  * uim一本で全ての入力:: http://www.d1.dion.ne.jp/~irino/osx/uim.html
  * [MacUIM](http://macuim.googlecode.com/)

### Maemo ###

Maemo CJK Support:: http://maemocjk.garage.maemo.org/

### Mandriva ###

公式パッケージが提供されています。 アーカイブがが細かく分割されているので、インストールし忘れには注意しましょう。

  * uim
  * libuim1
  * uim-gtk
  * uim-qtimmodule
  * uim-qt

インストールするには

```
# urpmi uim libuim1 uim-qtimmodule uim-qt
```

を実行してください。

### Momonga ###

公式パッケージが提供されています。 アーカイブが細かく分割されているので、インストールし忘れには注意しましょう。

  * uim
  * uim-devel
  * uim-xim
  * uim-fep
  * uim-emacs
  * uim-gtk
  * uim-qtimmodule
  * uim-qt4immodule
  * uim-scim
  * uim-anthy
  * uim-canna
  * uim-prime
  * uim-skk
  * uim-m17nlib
  * uim-applet
  * uim-qt

インストールするには

```
# yum install uim uim-gtimmodule uim-anthy uim-qt
```

を実行してください。

### NetBSD ###

pkgsrcに入っています。

```
# cd pkgsrc/inputmethod/uim
# make install clean
```

とすると、インストールされます。

インストールオプションはPKG\_OPTIONS.uim変数を設定することで変更します。/etc/mk.confに設定するか、

```
# env PKG_OPTIONS.uim='anthy eb qt' make install clean
```

などとして下さい。 デフォルトは、anthy cannaです（options.mk参照）。

### OpenBSD ###

http://openports.se/inputmethods/uim

### [OpenSolaris](http://www.opensolaris.org/) ###

http://www.opensolaris.org/os/project/input-method/files/

### openSUSE ###

[公式パッケージ](http://www.novell.com/products/linuxpackages/opensuse/uim.html)が提供されています。 アーカイブが細かく分割されているので、インストールし忘れには注意しましょう。

  * uim
  * uim-devel
  * uim-gtk2
  * uim-qt

### PC-BSD ###

  * http://www.ofug.net/~yamajun/files/
  * http://forums.pcbsd.org/viewtopic.php?p=39190

### Plamo ###

Plamoでは[contrib](ftp://ftp.linet.gr.jp/pub/Plamo/Plamo-4.5/contrib.old/FEP/)にあるようです。 設定方法などは[uim-memo.txt](ftp://ftp.linet.gr.jp/pub/Plamo/Plamo-4.5/contrib.old/FEP/uim-memo.txt)に書かれていますし、便利なパッチが適用されています。

### Slackware ###

[Slackware Add-on package Project](http://sourceforge.jp/projects/sap/)でuimのパッケージが配布されています。

  * http://groups.google.com/group/uim-ja/t/54448a0efcc10fe0

### Vine ###

'''4.0にupgradeしたらuimが動かなくなった'''という方を多数見かけますので、注意してください。

Vine 4.0ではVine Plusに含まれています。 アーカイブが細かく分割されているので、インストールし忘れには注意しましょう。

  * uim
  * uim-gtk
  * uim-xim
  * uim-fep
  * uim-el
  * uim-qt-immodule
  * uim-anthy
  * uim-canna
  * uim-mana
  * uim-skk
  * uim-qt
  * uim-applet

インストールするには

```
# apt-get install uim uim-gtk uim-anthy
```

を実行してください。

次にsetimeを実行してください。

```
$ setime uim
```

後は再ログインすれば使えるようになります。

### Windows（Cygwin） ###

Cygwinでuim:: http://www.d1.dion.ne.jp/~irino/windows/cygwin-uim.html

### Zaurus ###

  * http://sourceforge.jp/projects/openzaurus-ja
  * http://pdaxrom.sourceforge.jp/feed/