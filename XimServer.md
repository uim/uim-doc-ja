= XIM サーバ =

[uim:xim/README](http://uim.googlecode.com/svn/trunk/xim/README)より転載



## [UimXim](UimXim.md)に関して ##

uimパッケージは、[UimXim](UimXim.md)という名のXIMサーバを含んでいます。

XIMはレガシープロトコルで、多くの厳しい制限があります。しかしながら、多くのソフトウェアは、日本語のテキスト入力にXIMプロトコルのみをサポートします。したがって、私は一時的なツールとして[UimXim](UimXim.md)を書きました。

現在、[UimXim](UimXim.md)には多くの欠陥があります。それらのうちのいくつかは直すことができます。しかし、現実に行くべき道はXIM自体を捨てることです。

  * 私たちは、既にuimのGTK+とQt immoduleバージョンを持っています。


---


uim package includes an XIM server named uim-xim.

XIM is a legacy protocol and has many severe restrictions. However, there are many software which support only XIM protocol to input text especially in Japanese. So, I had written uim-xim as a tentative tool.

Currently, uim-xim has many defects. Some of them can be fixed. But the real way to go is to discard XIM itself.

  * We already have GTK+ and Qt immodule version of uim.

## [UimXim](UimXim.md)の主な欠陥 ##

それは文字がクライアントアプリケーションのワーキングエンコーディングに変換可能な言語を備えた入力方式のみをサポートします。要するに、クライアントアプリケーション（[OpenOffice](http://www.openoffice.org/).org、tgif…）がja\_JP.eucJPロケールで動作しているなら、あなたは日本語入力方式（anthy、prime、skk…）しか使用することができません。

しかし、UTF-8ロケール（ja\_JP.UTF-8など）でこれらのクライアントアプリケーションを使用するなら、あなたは利用可能なすべての多言語入力方式を使用でき、それらを動的に切り換えることができます。


---


It only supports input method with language whose character is convertible into the working encoding of client application. In short, if the client application (such as [OpenOffice](http://www.openoffice.org/).org, tgif...) is working with ja\_JP.eucJP locale, you can use only Japanese input methods (anthy, prime, skk...).

But if you use these client applications with UTF-8 locale (such as ja\_JP.UTF-8), you can use all the available multi-linguistic input methods, and switch them dynamically.

## どう[UimXim](UimXim.md)を使用するか ##

(1) [UimXim](UimXim.md)を起動してください。あなたは--engine=ENGINEコマンドラインオプションでスタートアップ変換エンジン(入力方式)を選択できます（ENGINEをanthy、prime、skk、tcode、tutcode…に読み換えてください。[UimXim](UimXim.md) --listで起動すると利用可能なエンジンの一覧を得られます）。 また、あなたは[UimPref](UimPref.md)ツールで標準の変換エンジンを指定できます。 上記二つの方法で指定しない場合、[UimXim](UimXim.md)のスタートアップロケールに対応した都合のよいエンジンが自動的に使われます。

(2) XMODIFIERS=@im=uimをセットして、クライアントを実行してください。

(3) 標準ツールキット1以外の候補ヘルパープログラムを使用したい場合は、[UimXim](UimXim.md)を起動する前にUIM\_CANDWIN\_PROG環境変数をセットしてください。

```
sh:  UIM_CANDWIN_PROG=uim-candwin-qt; export UIM_CANDWIN_PROG
csh: setenv UIM_CANDWIN_PROG uim-candwin-qt
```

何も指定しなかった場合、選ばれたツールキットに従いuim-candwin-gtkまたはuim-candwin-qtが標準になります。uimがGTK+またはQtで構成されていなければ、候補ヘルパーは使用されません。

(4) 変換エンジンを動的に変更するには、[UimImSwitcher](UimImSwitcher.md)ツールを使用してください。

(5) 入力コンテキストを動かす大部分は、[UimPref](UimPref.md)-{gtk,qt}によって動的に設定可能です。


---


(1) Invoke uim-xim. You can choose startup conversion engine (input method) with --engine=ENGINE command line option (replace ENGINE with anthy, prime, skk, tcode, tutcode... You can get list of available engines with invoking uim-xim --list). Also you can specify default conversion engine with uim-pref tool. Unless specifying with above two methods, preferred engine corresponding to startup locale of uim-xim is used automatically.

(2) Set XMODIFIERS=@im=uim and run client.

(3) If you want to use candidate helper program other than default toolkit one, set UIM\_CANDWIN\_PROG environmental variable before invoking uim-xim.

```
sh:  UIM_CANDWIN_PROG=uim-candwin-qt; export UIM_CANDWIN_PROG
csh: setenv UIM_CANDWIN_PROG uim-candwin-qt
```

If nothing specified, uim-candwin-gtk or uim-candwin-qt becomes default depending on the selected toolkit. If uim is not configured either with GTK+ or Qt, candidate helper is not used.

(4) To change conversion engines dynamically, use uim-im-switcher tool.

(5) Most setting of working input contexts are dynamically configurable by uim-pref-{gtk,qt}.

## どう特別の修飾キーを使用するか ##

uimは、カスタマイズされたキーオペレーション用の'Super'および'Hyper'修飾キーをサポートします。機能を使用可能にするためにステップに従ってみてください。

(1) SuperとHyperキーに任意のキーをマップします。

```
xmodmap -e 'keycode 115 = Super_L'      # 左Windowsキー
xmodmap -e 'keycode 116 = Super_R'      # 右Windowsキー
xmodmap -e 'add mod3 = Super_L Super_R' # どのmod番号でもOK

xmodmap -e 'keycode 117 = Hyper_L'      # 「アプリケーション」キー
xmodmap -e 'add mod4 = Hyper_L'         # どのmod番号でもOK
```

(2) [UimPref](UimPref.md)であなた自身のキー設定を定義します。


---


uim supports 'Super' and 'Hyper' modifier keys for customized key operations. Try following steps to enable the feature.

(1) map arbitrary keys to Super and Hyper keys

```
xmodmap -e 'keycode 115 = Super_L'      # left Windows key
xmodmap -e 'keycode 116 = Super_R'      # right Windows key
xmodmap -e 'add mod3 = Super_L Super_R' # any mod number is OK

xmodmap -e 'keycode 117 = Hyper_L'      # 'Application' key
xmodmap -e 'add mod4 = Hyper_L'         # any mod number is OK
```

(2) define your own key-bindings with uim-pref.

## 一時的にuimを迂回する ##

uimは、uimを一時的に迂回するための'emergency key'特徴を持っています。 これはいくつかのアプリケーションで役に立ちます。また、言語変換を避けるもう一つの方法は、[UimImSwitcher](UimImSwitcher.md)ツールかキーボードショートカットを使用するIM反転機能を使用して、「直接入力」入力方式を選ぶことです。私たちは後者の方法を推奨します。

  * 'emergency key'を使用する方法

(1) [UimXim](UimXim.md)を起動する前に、以下の環境変数をセットしてください。

```
LIBUIM_ENABLE_EMERGENCY_KEY=1
```

(2) uimのキー処理を無効/有効にするためにShift+Backspaceを押してください。 uimのキー処理がemergency keyによって無効になっている間、キー入力は直接アプリケーションに渡されます。


---


uim has 'emergency key' feature to bypass uim temporarily. This is useful with some applications. Also another way to avoid language conversion is choosing "direct" input method using uim-im-switcher tool or IM-toggle facility using keyboard shotcuts. We recommend latter method.

  * The way to use 'emergency key'

(1) Set following environment variable before invoking uim-xim.

```
LIBUIM_ENABLE_EMERGENCY_KEY=1
```

(2) Press Shift + Backspace to disable/enable uim key processing. Key inputs are directly passed to applications while uim key processing is disabled by emergency key.

## XIMイベントフローについて ##

[UimXim](UimXim.md)は二種類のXIMイベントフロー方法、（kinput2、skkinput2…に似た）full-synchronous-methodと（SCIMのx11フロントエンドやIMdkitを使用するXIMサーバーに似た）on-demand-synchronous methodをサポートします。[UimXim](UimXim.md)は、標準でfull-synchronous-methodを使用するように設定されています。いくつか特定のXIMクライアントアプリケーションを使用している間、時々XIM\_ERRORと共にerror\_code=13を受け取るなら、'--async'コマンドラインスタートアップオプションを加えてon-demand-synchronous methodを使用するようにしてください（注意:on-demand-synchronous methodはTcl/Tkバージョン8.{3,4}現在のXIM実装では働きません）。


---


uim-xim supports two XIM event flow methods, full-synchronous-method (like kinput2, skkinput2...) and on-demand-synchronous method (like XIM server using IMdkit, such as SCIM's x11 frontend). Default behavior of uim-xim is set to use full-synchronous-method. If you get occasional XIM\_ERROR with error\_code = 13 while using some specific XIM client applications, please try to use on-demand-synchronous method with adding '--async' command line startup option (Warning: on-demand-synchronous method is known to not work with current XIM implementation of Tcl/Tk version 8.{3,4}).

## 内部実装 ##

[UimXim](UimXim.md)は内在的理由でUTF-8としてすべてのIM関連の文字列を処理します。XIMクライアントアプリケーションがja\_JP.UTF-8などのUTF-8ロケールで動く時、文字列は以下の通り変換されます。

  * 「foo」は、fooにコード化された文字列を表現します。

```
uim-anthy (only for example)
   |
   v
"EUC-JP"
   |
   v
libuim (iconv(3))
   |
   v
"UTF-8"
   |
   v
uim-xim (XmbTextListToTextProperty)
   |
   v
"compound text"
   |
   v
XIM client
```

また、[UimXim](UimXim.md)はja\_JP.eucJPなどの非UTF-8のネイティブロケールで動いているXIMクライアントをサポートします。クライアントアプリケーションがそのようなロケールで動いていると、以下のように何らかのエンコーディング変換が起こります。

```
uim-anthy (only for example)
   |
   v
"EUC-JP"
   |
   v
libuim (iconv(3))
   |
   v
"UTF-8"
   |
   v
uim-xim (iconv(3))
   |
   v
"EUC-JP"
   |
   v
uim-xim (XmbTextListToTextProperty)
   |
   v
"compound text"
   |
   v
XIM client
```

このような場合、実装において文字列を処理するために、[UimXim](UimXim.md)はUTF-8を通してさらなる変換を行います。しかし、'native->UTF-8'と'UTF-8->native'両変換が同じiconv(3)コンバータによって行なわれるので、キャラクタコード変更が生じないことは保証されます。この結果、以下の通りにja\_JP.eucJPエンコーディングで動く古い実装と同等の正確な文字列が生じます。

```
uim-anthy (only for example)
   |
   v
"EUC-JP"
   |
   v
libuim (iconv(3))
   |
   v
"EUC-JP"
   |
   v
uim-xim (XmbTextListToTextProperty)
   |
   v
"compound text"
   |
   v
XIM client
```


---


uim-xim processes all IM-related strings as UTF-8 for internal reasons. When a XIM client application runs on an UTF-8 locale such as ja\_JP.UTF-8, the strings are converted as follows.

  * "foo" expresses a string encoded in foo.

```
uim-anthy (only for example)
   |
   v
"EUC-JP"
   |
   v
libuim (iconv(3))
   |
   v
"UTF-8"
   |
   v
uim-xim (XmbTextListToTextProperty)
   |
   v
"compound text"
   |
   v
XIM client
```

uim-xim also supports XIM clients working on non UTF-8 native locales such as ja\_JP.eucJP. When a client application runs on such locales, some additional encoding conversion occurs as follows.

```
uim-anthy (only for example)
   |
   v
"EUC-JP"
   |
   v
libuim (iconv(3))
   |
   v
"UTF-8"
   |
   v
uim-xim (iconv(3))
   |
   v
"EUC-JP"
   |
   v
uim-xim (XmbTextListToTextProperty)
   |
   v
"compound text"
   |
   v
XIM client
```

In such case, uim-xim performs an additional conversion via UTF-8 to process the strings in the implementation. But it is ensured that no character code alteration will occur since the both 'native->UTF-8" and 'UTF-8->native' conversions are performed by same converter iconv(3). This results the string as accurate as the old implementation which is dedicated to ja\_JP.eucJP encoding as follows.

```
uim-anthy (only for example)
   |
   v
"EUC-JP"
   |
   v
libuim (iconv(3))
   |
   v
"EUC-JP"
   |
   v
uim-xim (XmbTextListToTextProperty)
   |
   v
"compound text"
   |
   v
XIM client
```