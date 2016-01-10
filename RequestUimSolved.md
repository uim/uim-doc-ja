= 解決済みの要望 =



## 解決された機能 ##


### 記号一覧入力 ###

記号一覧入力する時に使うような、10x4ぐらいの大きさのウィンドウ これができたらT-codeのストローク図示に使います。-- 64@2ch


---


散々待たせておいてこんな返事で申し訳ないのですが、どういうものが欲しいのか詳しく説明してもらえますか？--tkng


---


こんなやつを表示するウィンドウです。よくカーソル移動で選択してEnterで文字がでてくる、みたいな -- 64@2ch

```

 A1A0 、。，．・：；？！゛゜´｀¨
 A1B0 ＾￣＿ヽヾゝゞ〃仝々〆〇ー?‐／
 A1C0 ＼〜‖｜…‥‘’“”（）〔〕［］
 A1D0 ｛｝〈〉《》「」『』【】＋−±×

```

上のようなものがあればT-codeの場合には以下の例のように応用します。例は第一打鍵に「k」を打った場合の第二打鍵を表したストローク表です。 -- 64@2ch

```

 突周景雑杉 ■奏■■■
 どル (日 8 井集ツ打品
 ○たの 0に 水教エ天書
 円社 _ 9会 用商ポ党ヌ

```


---


理解はできましたが、実装は難しい気がします。--tkng


---


(´・ω・`)ショホ゛ーン 記号一覧入力って時代遅れなのかな --64@2ch


---


記号一覧入力がダメだというわけではないのですが、コンソールなどでの利用を考えると実装方法が思い付きません。外部プログラムで対応することになるかなぁ。--tkng


---

1.6.0 で tutcode 向けの候補ウィンドウが実装されました。

### uim-skk + azik 二重母音の送り仮名指定 ###

uim+azik で二重母音がシフト入力された場合、後の母音を 送りがなとして判定してほしい。

### 句読点入力時の自動変換開始機能 ###

AnthyやManaで句読点を入力したら、自動的に変換を始める機能が欲しいです。

### ローマかなテーブルの調整 ###

http://pc11.2ch.net/test/read.cgi/linux/1135968795/759

```

「la(ぁ)」なのに、「lyx(りゃ)」なのは統一感がないとおも。
「xwi(ゐ)」「xwe(ゑ)」はSKK由来(?)っぽいけど、「xyi(ゐ)」「xye(ゑ)」に移動したほうがいいとおも。

```

元759ですが「wyi(ゐ)」「wye(ゑ)」の間違いです。

ついでにdwa、kwa等を拡張する案を。 既に含まれているもの。

  * kwa(くぁ)
  * gwa(ぐぁ)
  * swa(すぁ)
  * twa(とぁ)
  * dwa(どぁ)
  * hwa(ふぁ)

以下を拡張。

  * zwa(ずぁ)
  * nwa(ぬぁ)
  * bwa(ぶぁ)
  * pwa(ぷぁ)
  * mwa(むぁ)
  * ywa(ゆぁ)
  * rwa(るぁ)

この規則性に合わせると

  * twa(とぁ)→twa(つぁ)
  * dwa(どぁ)→dwa(づぁ)

とする方が自然です。

これも追加希望。

  * hwyu(ふゅ)
  * vwa(う゛ぁ)
  * vwi(う゛ぃ)
  * vwu(う゛ぅ)
  * vwe(う゛ぇ)
  * vwo(う゛ぉ)
  * hwu(ふぅ)

### 英和/和英辞書統合 ###

http://lists.sourceforge.jp/mailman/archives/anthy-dev/2004-February/000516.html

### kinput2風の入力モード表示スタイル ###

http://www.fenix.ne.jp/~G-HAL/soft/nosettle/#uim


---


[r5709](http://groups.google.com/group/uim-commit/browse_thread/thread/a2c96a4cfed6821f)で対応済み。

### ホットキーによる IM の トグルについて ###

[r1868](http://lists.freedesktop.org/pipermail/uim-commit/2005-October/001739.html) でホットキーによって2つの IM をトグルできるようになりましたが、 そうではなくて、3つ以上の IM を循環するようになって欲しいです。 あと、「Alternative input method」というのは必要なくて、 「使用可能にする入力方式」だけで良いような気もします。


---


その機能なら既にありますよ。 im-custom.scmのim-switching下のコメントになっている部分を外した後、 uim-prefで設定すれば使えます。 ついでですが、その部分にはこう書いてあります。

```

;; I think that current "im-switching by hotkey" feature is not
;; useful. So commented out them to avoid confusion of users.
;;   -- YamaKen 2005-02-01

```


---


r1868の変更を取り消した上で、上記コメントアウトされているコードを有効にして試してみました。 「入力モードをカーソルの近くに表示する」にチェックを入れていると、 IM を切り替えた直後は一つ前の IM の状態が表示されるバグがあるようです。 切り替えたあとにその IM での状態を変更するとちゃんと表示されるのですが。 ([r1868](http://lists.freedesktop.org/pipermail/uim-commit/2005-October/001739.html)の変更はそういったことも考慮しているようですが…)


---


1.5.2で対応済み。

### uim-texが欲しい ###

http://deruose.blogspot.com/2007/03/tex-vs-uim.html


---


リンク先が404なので詳細不明。

### T-Codeで交ぜ書き変換や部首変換したい。 ###

[T-Code仕様書](http://web.sfc.keio.ac.jp/~p92395kk/Input/t-code.html)


---


[r4553](http://groups.google.com/group/uim-commit/browse_thread/thread/56ab5f41693486f1)

uim-tutcodeの設定"Code table file"に"tcode.scm"を指定。

### uim-anthyの半角英数入力モードの名前 ###

anthyでは「半角英数モード」になってます。canna、manaと統一したほうがいいのでは?


---


[r4778](http://groups.google.com/group/uim-commit/t/44b9242213bab90c)で修正されました。

### viに適応した入力制御を使用する ###

「viに適応した入力制御を使用する」をAnthyやPRIMEでも使えるようにして欲しい。


---


[r913](http://lists.freedesktop.org/archives/uim-commit/2005-July/000793.html), [r1197](http://lists.freedesktop.org/archives/uim-commit/2005-August/001077.html), [r1203](http://lists.freedesktop.org/archives/uim-commit/2005-August/001083.html)

### uim-candwin-gtk/qtやuim-helper-serverをlibexecに移動 ###

基本的に直接実行しないものはlibexecに移動して欲しい。


---


[r1490](http://lists.freedesktop.org/archives/uim-commit/2005-September/001370.html)

### かな入力で「ー」 ###

かな入力で「ー」を入力すると「ーー」のように二つでてしまうのをなんとかしてほしい


---


0.4.5で修正済み。

### skkの個人辞書のセーブをサポートして欲しい ###

0.0.8で対応済み。

### AnthyのF6〜F10をMS-IMEライクにして欲しい。 ###

[anthy-dev:760](http://lists.sourceforge.jp/mailman/archives/anthy-dev/2004-April/000759.html)

MS-IMEの機能とはちがって、今実装されているこの機能は、 確定前の文字列を全部カタカナなどにしてしまいますが、 実際には文節ごとに、カタカナに変換とかをできるようにしてほしい。

1.2.0-alphaではそのような動作になっています。

### skkserv ###

skkservをサポートして貰えると嬉しいです。SKK-JISYO.Lを読むと10秒くらいかかるので…


---


[anthy-dev:1962](http://lists.sourceforge.jp/mailman/archives/anthy-dev/2005-March/001961.html), [anthy-dev:1964](http://lists.sourceforge.jp/mailman/archives/anthy-dev/2005-March/001963.html) でパッチが出されました。


---


[r826](http://lists.freedesktop.org/archives/uim-commit/2005-April/000706.html)にてコミットされました([anthy-dev:2013](http://lists.sourceforge.jp/mailman/archives/anthy-dev/2005-April/002012.html))。0.4.7で選択できるようになっています。

### 自動変換機能(skk) ###

skkで▽モードのときに「を」、「、」、「。」などを入力したときに自動で変換してくれる機能が欲しいです。 --662


---


0.4.6で使えるようになりました。

### skkで「/」を含むものが辞書に登録出来ないです。 ###

skkで「/」を含むものが辞書に登録出来ないです。例えば<br />を「かい」で登録した場合、ddskkでは「かい/(concat "<br ?057>")/」というような形で辞書に載るのですが、uim-skkでは既に登録してあるものを変換すると「(concat…」というのがそのまま表示されてしまいます。


---


これも0.4.6で使えます。


---


ありがとうございます。

### skkのazik入力対応。 ###

[anthy-dev:1922](http://lists.sourceforge.jp/mailman/archives/anthy-dev/2005-March/001921.html)

### uim-skkでshift+spaceを何にも割り当てて「いない」時、 ###

uim-skkでshift+spaceを何にも割り当てて「いない」時、0.4.5ではどのモード中でもアプリケーションに渡っていましたが、0.4.6ではラテン語モード以外では渡らなくなってしまいました。何にも使っていない時はアプリケーションに渡して欲しいのですが…。


---


すみませんです。不注意で消してしまっていました。[svn revision 793](http://lists.freedesktop.org/archives/uim-commit/2005-March/000673.html) で直しておきました (0.4.7では直っています)。

### 候補ウィンドウで注釈とかを表示してウザがられたい ###

0.4.6 で [EB ライブラリ](http://www.sra.co.jp/people/m-kasahr/eb/index.html) を用いた注釈の検索・表示がサポートされました。([anthy-dev:1790](http://lists.sourceforge.jp/mailman/archives/anthy-dev/2005-February/001789.html))

### asdfで候補選択をできるようにして欲しいです。 ###

http://openlab.ring.gr.jp/skk/skk-manual/skk-manual-ja_5.html#SEC85のようなもの。


---


[anthy-dev:2019](http://lists.sourceforge.jp/mailman/archives/anthy-dev/2005-May/002018.html)でuim-skkに対するパッチが作られました。


---


[r831](http://lists.freedesktop.org/archives/uim-commit/2005-May/000710.html)にてコミットされました([anthy-dev:2022](http://lists.sourceforge.jp/mailman/archives/anthy-dev/2005-May/002021.html))。 0.4.7では、uim-pref から選べるようになっています。

### uim-skk: X で辞書エントリの削除 ###

元祖 skk のように、 候補表示中の X で、現在の候補を辞書から削除できると嬉しいです。 これがあれば、とりあえず辞書編集機能は不要だと思いますし。--nakanot ----- [r938](http://lists.freedesktop.org/archives/uim-commit/2005-July/000818.html), [r939](http://lists.freedesktop.org/archives/uim-commit/2005-July/000819.html) でサポートされました。[anthy-dev:2129](http://lists.sourceforge.jp/mailman/archives/anthy-dev/2005-July/002128.html) 参照。

### Macromedia Flashのアプリでキーボード入力や操作をするとブラウザごと固まる。 ###

入力メソッドをkinput2やscimにすると固まらなくなるので、uimのせいだと思うのですが。。


---


もう少し環境を書かれてはどうでしょうか。


---


ためしたのは

ディストリビューション:Vine Linux 3.2 kernel 2.4.31-0vl1.12。 バージョン:apt-getでもってきたuim-0.4.1と公式から落してきてビルドしたuim-1.0.1。 ブラウザ:Mozilla 1.7.8, Mozilla Firefox 1.5, 風博士 0.1.9, Konqueror 3.5 (すべてFlash Player 7.0r61)。 デスクトップ:GNOME 2.4。

でいずれもだめでした。 他に書くべき環境はございますでしょうか？


---


報告ありがとうございます。手元でも再現する環境とそうでない環境があったのですが、とりあえず直しておきました。http://lists.freedesktop.org/archives/uim-commit/2006-January/002848.html のパッチを当ててみてください (加藤)。


---


ありがとうございます。 修正を確認いたしました。 わたしの環境のみかもしれませんが Flashアプリでキー入力が必要なところでは、左クリックでは なく右クリックでフォーカスすれば入力できるようです。

### アプレットからも変換方式を変えられるようにして欲しい。 ###

[r3088](http://lists.freedesktop.org/pipermail/uim-commit/2006-February/002945.html)で、ツールバーのアイコンから選択して変更できるようになりました。 (http://lists.freedesktop.org/pipermail/uim/2006-February/001429.html)

### 入力モードをもっと識別しやすく ###

uim-anthyの場合

```

a(直接入力)、あ(ひらがな)、ア(カタカナ)、ア(半角カタカナ)、ａ(全角英数)

```

となっていますが、使用しているフォントによっては識別しづらい事もあるで、半角文字の入力モードは先頭にアンダースコアを入れてみてはどうでしょうか。

```

_a(直接入力)、あ(ひらがな)、ア(カタカナ)、_ア(半角カタカナ)、ａ(全角英数)

```

と。

こっちは好みの問題ですが、uim-skkはオリジナルのSKKに合わせて

```

SKK(直接入力)、かな(ひらがな)、カナ(カタカナ)、全角(全角英数)

```

とか、skk-isearchの入力モード表示に使われている

```

aa(直接入力)、か(ひらがな)、カ(カタカナ)、英(全角英数)

```

にするのはどうでしょうか。


---


uim-1.1.0-alphaでアイコンがサポートされているようです。

### uim-primeで英語と日本語の予測入力動的切り替え ###

scim-primeではツールバーから動的に切り替えて使えます。 uim-primeでも同じように使えたら便利だと思いますが。


---


F11 キーで動的に切替え可能です。またキーは変更もできます。[r3853](https://code.google.com/p/uim-doc-ja/source/detail?r=3853) で ツールバーから言語変更できるようにしておきました。

### 仏語，ロシア語など ###

仏語，ロシア語などアルファベットが違いますがそういったモードはありますか？


---


uim-elatin, uim-latin あるいは、uim-m17nlib を介して利用可能です。

### 候補ウィンドウの配色 ###

http://lists.sourceforge.jp/mailman/archives/anthy-dev/2004-October/001275.html


---


新しめの GTK+ では再現しなくなってます。

### 候補ウィンドウにおける変換候補の表示のずれ ###

http://lists.sourceforge.jp/mailman/archives/anthy-dev/2004-November/001395.html


---


新しめの GTK+ では再現しなくなってます。

### uim AZIK+SKK "q"キーをカタカナ変換に使う ###

http://lists.sourceforge.jp/mailman/archives/anthy-dev/2004-October/001258.html


---


[Bug 1732](https://bugs.freedesktop.org/show_bug.cgi?id=1732)

### 黒背景だとツールバーのアイコンの文字が見えない ###

http://pc11.2ch.net/test/read.cgi/linux/1135968795/898

```

システムトレイに格納して利用してますが
入力モードの文字色を変更することができませんでしようか？
現在 Gnome 上でテーマの色を黒にしているので
テーマ色と同化して全く見えなくなってしまいます。

```


---

「ツールバー」設定の「濃色背景向けアイコンを使用する」を有効にしてください。


### ツールバーをIMオン/オフで表示/非表示 ###

http://pc11.2ch.net/test/read.cgi/linux/1200850880/101

```

uim-toolbar-(gtk|qt)を
日本語入力ON→表示
日本語入力OFF→非表示
することってできませんか?

```

uim 1.8.0で対応しました。

### GUIで変換テーブルのカスタマイズ ###

今のところ~/.uimに手書きするしか方法がないので欲しいです。 ~/.uimがあるとuim-pref-gtkがいちいち警告を出すのでうっとおしいですし。

uim 1.8.0で対応しました。

### sticky shiftを使いたい ###

[sticky^shift](http://homepage1.nifty.com/blankspace/emacs/sticky.html)

uim 1.8.2で対応しました。

## その他 ##

### uim-skk: Shift-space と C-j の区別 ###

Shift-space で skk システムを off にしたら、 C-j がアプリケーションに直接渡るようにはできないでしょうか。 詳細は http://surf.ap.seikei.ac.jp/~nakano/diary/?20050630#200506308 に書いておきました。 --nakanot


---


uim-im-switcher で、その rxvt の入力方法を一時的に direct あるいは latin にするか、mlterm のように起動中にでも IM を on/off できるようなターミナルを使ってみてはいかがでしょうか?


---


[r1868](http://lists.freedesktop.org/archives/uim-commit/2005-October/001739.html)でホットキーによりIMをトグルできるようになっています。