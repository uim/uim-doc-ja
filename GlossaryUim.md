= 用語 =

uimで使われる用語

tkng氏が書いた[Glossary](http://lists.freedesktop.org/archives/uim/2005-August/001314.html)に続くスレッドから転載。



## preedit（編集領域） ##

「編集領域」は、まだアプリケーションに入力されていない文字列をいい、 ユーザーに入力コンテキストの状態を教える。 o-umlautを入力する場合、「Multi\_key o "」のようなキー列を入力する。 「o」を入力した時点では何を入力するか決定できない（「o」のあとに 「'」がきたらo-accute が入力され、「`」がきた場合はo-grave が入力される）。

多くの場合、編集領域は下線のついた背景が反転した状態でカーソル位置に 表示される。

編集領域は複数の文字からなることがあることにも注意。


---


Preedit is a string which is not yet input to an application. It is appeared to inform user about input state of the input context. For example, to input o-umulaut, following key sequence is used.

```
Multi_key, o, "
```

When o was input, what sould be input could not be determined. (When ' come after o, then o-accute will be input. When ` come after o, then o-grave will be input.)

In most cases, preedit is displayed at the cursor position with underline or reversed background color.

Note that preedit may be consist of multiple characters.

## commit（確定） ##

実際に入力される文字列について入力コンテキストが決定すると、 [LibUim](LibUim.md)はアプリケーションに「こういう文字列が入力された」と伝える。

この動作を「確定」と呼ぶ。 確定された文字列は最終的な「編集領域」の文字列とは異なることが多い。 二つの文字列の等価性についてはいかなる仮定もおくべきではない。


---


Once an input context get determined about the characters which should be input actually, libuim tells to the application that 'these characters have been input'.

This action is called 'commit'. The string which will be committed to often differs from the latest 'preedit' string. Any assumption about an equivalence between the two strings **MUST NOT** be applied.

## segment ##

uimでは「segment」は分節された文の部分をいう。 Anthyでは、変換時の編集領域はひとつ以上のsegmentからなり、 各segmentは一つの句からなる。 segmentはsegmentごとの処理の単位にもなる。


---


In uim, segment often means a segmented part of a sentence. For example, in Anthy, converting-phase preedit is represented as a sequence of one or more segments that each segment holds a phrase. A segment provides a unit which per-segment operations can be applied to.

## candidate（候補） ##

多くの場合、編集領域一つに対して変換候補は複数ある。 例えば日本語では、最初にひらがなを入力し次にそれを漢字に変換する。 このとき、たいていは複数の候補から一つを選ばなければならない。 このような場面で「候補」を使う。

厳密に言えば、「変換」候補である必要はない。 例えば、PRIMEでは、候補は変換ではなく予測の結果になる。


---


Frequently one preedit has plural conversion candidate. For example, in Japanese, at first we input Hiragana (phonogram of Japanese), then convert them to Kanji (Ideogram of Japanese). At the time of converting, often we need to select one candidate from selections. Candidate is used in such situation.

To be exact, it need not be 'conversion' candidate. For example, in the case of PRIME, candidate is guessed rather than the result of conversion.

## context ##

コンテキストは入力の単位である。 入力コンテキストと呼ぶこともある。 通常、テキストウィジェット一つにコンテキストは一つである。 しかし、アプリケーションによっては、複数のテキストウィジェットが 一つの入力コンテキストを共有することもある（例えばMozilla）。


---


Context is a unit of inputting. This is sometimes called as 'input context'. Normally, one text widget has one context. But in some application, plural text widgets share one input context. (e.g. Mozilla.)

## bridge ##

bridgeはアプリケーションとuimの繋ぎのコードである。 uimには沢山のbridgeがある。

  * GTK+ bridge (GTK+ immodule)
  * Qt bridge (Qt immodule)
  * XIM bridge (uim-xim)
  * Console bridge (uim-fep)
  * Emacs bridge (uim.el)
  * Mac bridge (MacUIM)


---


Bridge is a glue code between applications and uim. There are many bridges on uim.

  * GTK+ bridge (GTK+ immodule)
  * Qt bridge (Qt immodule)
  * XIM bridge (uim-xim)
  * Console bridge (uim-fep)
  * Emacs bridge (uim.el)
  * Mac bridge (MacUIM)

## plugin ##

「プラグイン」はuimのSchemeインタプリタをCで拡張するための仕組みで、 主にAnthyのような変換ソフトとuimの繋ぎのコードを書くのに使われる。

http://lists.freedesktop.org/archives/uim/2005-August/001316.html

プラグインという言葉は多くの場合「アプリケーションの拡張機能で、 単一のオブジェクトファイルからなるもの」を指すことが多いので、 uim用のfoo.soのようなものは、混乱を避けるためにも プラグイン以外の名前で呼んだ方がいいと思う。

また、後で述べるが、uimの拡張機能を有効にするのに 複数のファイルが必要になることもあり、 これも既存のプラグインの概念と衝突する。


---


Plugin is a mechanism to extend uim's Scheme interpreter with C. Mainly used to write a glue code between uim and conversion software such as Anthy.

http://lists.freedesktop.org/archives/uim/2005-August/001316.html

Since the term 'plugin' often means that "a extension for an application that CONSIST OF SINGLE OBJECT FILE", I think that foo.so for uim should be renamed to other than 'plugin' to avoid confusions.

As I described below, uim sometimes requires multiple files to enable an extension. This conflicts with the ordinary plugin concept.

## helper ##

ヘルパーはuimの暗黒面で、次のような意味で使われている言葉である。

  1. プロセス間通信に関するもの
  1. coreでもbrideでもないもの

この二つは混同されるべきではないし、「ヘルパー」という名前も 直感的ではない。

そこで、この単語をできるだけ使わないことに決めた。 例えば、0.5系列ではプロセス間通信に関する部分には message busという新しい名前をつけるつもりだ。


---


Helper is a dark side of uim. Helper is an identifier used in:

  * (a) Which are related on inter process communication
  * (b) Which are neither core nor bridge

(a) and (b) should not be identified with the same identifier. In addition, 'helper' is not intuitive.

Therefore now we make an effort to reduce the use of this word. For example, in 0.5 series, most of the code which related on inter process communication will be given new identifier 'message bus'.

## input context ##

「入力コンテキスト」は入力の単位である。 「コンテキスト」と略すこともある。


---


Input context is a unit of inputting. The word is sometimes abbreviated as 'context'.

## input method（入力方式） ##

  1. キーボードから直接入力できない文字列を入力するソフトウェア
  1. uimの標準インタフェース上につくられたモジュールで、（キー入力）イベントを何らかのテキストに変換するもの


---


  1. A software to input characters which cannot input from keyboard directly.
  1. A modular unit of uim built on the standard interface that handles (key) events to transform them into some texts

## module ##

実際の入力と変換を扱う部分をこう呼ぼうと考えたこともあったが、 この表現は誤解を招きそうなので、この言葉に明確な定義を 与えないことにした。

http://lists.freedesktop.org/archives/uim/2005-August/001316.html

詳しくは後で考えるとして、今はこのようなものだと考えている。

  * 単位ごとにインストール・アンインストール、有効・無効にできるコードのまとまり
  * モジュールには0個以上の任意の入力方式が含まれる

これを踏まえて以下の例を見て欲しい。

### Anthy ###

anthyモジュールは三つのファイルからなり、 モジュールを有効にすると、副作用としてregister-imを一度呼ぶ。

  * anthy/anthy.so
  * anthy/anthy.scm
  * anthy/anthy-custom.scm

### m17nlib ###

m17nlibも三つのファイルからなるが、このモジュール一つを有効にすると register-imは複数回呼ばれる。

  * m17nlib/m17nlib.so
  * m17nlib/m17nlib.scm
  * m17nlib/m17nlib-custom.scm

### regexp ###

regexpモジュールは入力方式を含まないが、これも完全なモジュールである。 一つのファイルからなり、有効にすると普通の関数が定義される。

  * regexp/regexp.so


---


Once I planned to use this word as a name of the part which handle actual input and convert. But this word seems causing misunderstanding, therefore I decided that I don't give a clear definition of this word for now.

http://lists.freedesktop.org/archives/uim/2005-August/001316.html

For future consideration, my current recognition is:

  * A unit for a set of codes that allows install/deinstall and enable/disable based on the unit
  * A module may or may not contain arbitrary number of input method(s)

See following examples based on above definition,

1. anthy

anthy module will be consist of these 3 files. Enabling the module causes register-im as a side effect

  * anthy/anthy.so
  * anthy/anthy.scm
  * anthy/anthy-custom.scm

2. m17nlib

m17nlib module will also be consist of 3 files. But enabling the module causes multiple register-im even if only one module has been enabled.

  * m17nlib/m17nlib.so
  * m17nlib/m17nlib.scm
  * m17nlib/m17nlib-custom.scm

3. regexp

A regexp module will be also a complete module although it does not contain input method. It will be consist of only one file, and enabling it only causes ordinary procedure definition(s).

  * regexp/regexp.so