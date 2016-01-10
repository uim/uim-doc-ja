= 要望 =


欲しい機能をどんどんと書いていくページ。要望が多い機能は優先的に実装されるかも([解決済みの要望](RequestUimSolved.md))。



## 未解決の要望 ##

### anthyで文節を明示的に指定したい ###

### anthyで（「の」の連続）とか注意してウザがられたい ###

### uimアプレットで ###

uimアプレットでWindows等と同等の感覚で操作できるようになると嬉しいです。

### いまのアプレット GNOME の他のものと大きさが違う。 ###

いまのアプレット GNOME の他のものと大きさが違う。 このへんはGNOMEの流儀にしたがって欲しい。


---


いっしょの大きさだと思うんですけど…。--tkng


---


現状のuim-appletは縦パネルの場合が考慮されていません． パネルを縦にして，22ドットで確認してみて下さい．


---


パネルが縦の場合に対応する予定は今のところありません。--tkng


### イルカとか冴◯先生とか -- 64@2ch ###

私はOfficeの類はあんまり使わないのでよくわからないのですが、それはInputMethodとはレイヤが違うように思います。--tkng


---


元々冗談だったのですが、なんか欲しくなってきました。T-codeは難しいので見出付きヘルプシステムを表示するところが欲しいなと。 -- 64@2ch


---


グラフィックスイメージを表示する機能があればこんな表示もやりたいぞ。http://koringo.purose.net/wiki/?%5B%5BT-code%5D%5D -- 64@2ch


---


グラフィックスイメージによるUIはT-codeじゃなくてもマウス手書入力なんかで必要になってくるのだ -- 64@2ch


---


うーんこれってschemeから外部プログラムを呼び出せれば済むことかな。もしかして現在のuimでもできること? --64@2ch


---


とりあえずわかるところだけ。画像など非キーボードによる入力はサポートしたいところですが、libuimでやるにはtoolkitなどに依存する部分が多すぎます。落としどころとしては外部プログラムの起動のサポートと、別プロセスからの文字列のcommitのサポートぐらいでしょうか。ちなみに現在、外部プログラムの起動はできたように思いますが、別プロセスからの文字列のcommitは標準入出力を介してのみ可能です。(UnixDomainSocketによる通信では不可能）標準入出力を介する場合でもschemeだけでは不可能で、定型文ではあるものの、C言語を2,30行程度書く必要がでてきます。まだどういう風に改良するのが良いのかはちょっと思い付きません。--tkng


---


自分的にすぐ欲しい機能はcommit無のグラフィック表示なので、外部プログラムの起動を試してみようと思います -- 64@2ch

### 入力モード別にカーソルの色を替えられる機能が欲しい。 ###

http://openlab.ring.gr.jp/skk/skk-manual/skk-manual-ja_4.html#SEC19

```

「かなモード」
 * アスキー小文字をひらがなに変換するモード。
 * マイナーモードの表示: `かな'
 * カーソル色: 赤系

「カナモード」
 * アスキー小文字をカタカナに変換するモード。
 * マイナーモードの表示: `カナ'
 * カーソル色: 緑系

「全英モード」
 * アスキー小文字／大文字を全角アルファベットに変換するモード。
 * マイナーモードの表示: `全英'
 * カーソル色: 黄系

「アスキーモード」
 * 文字変換を行わないモード。
   入力されたキーは C-j を除いて通常の Emacs のコマンドとして解釈される。
 * マイナーモードの表示: `SKK'
 * カーソル色: 背景によりアイボリーかグレイ。

```

### キーバインド関係の見直しをして欲しい。 ###

標準のオン、オフキーにShift+SPCを含めない。 初期設定されているキーが多すぎる。

### uim-dictでskk個人辞書編集 ###

sumika時代は対応してたと思うんですけど…。

### uim-skk + azik 二重母音の送り仮名指定 ###

uim+azik で二重母音がシフト入力された場合、後の母音を 送りがなとして判定してほしい。

### ANK-漢字変換モードが欲しい ###

  * [boiled-egg](http://usir.kobe-c.ac.jp/boiled-egg/)
  * [YC](http://www.ceres.dti.ne.jp/~knak/yc.html)

### uim-anthyで逐次変換したい ###

既にscim-anthyでは実装されているのですが、便利なので欲しいです。 他にも連文節変換と単文節変換が選べる機能もあります。

### uim-ximが使用するuim-candwin-gtk/qtの選択をuim-prefで設定 ###

UIM\_CANDWINで指定できますけど、uim-prefにXIM設定って項目が増えたのでどうせなら。 現状gtk+でコンパイルすると、uim-candwin-gtkが起動するようになりますけど、もしuim-candwin-gtkが存在しなければuim-candwin-qtを起動するようになるとうれしい。

### スペースシフトへの対応 ###

  * [SandSキーお試しアプレット](http://hp.vector.co.jp/authors/VA002116/sands/index.html)
  * [さくら配列 スペースシフト](http://fiercewinds.net/siki/pub/2006/07/08_232521/)

### uim-toolbar-gtkとuim-toolbar-gtk-systrayの統合 ###

uim-toolbar-gtkをシステムトレイにDnDすると収納されるとか、その逆とかできたらうれしい。

### Egg v4にあるようなマルチフェンス機能 ###

現在の入力をプリエディットの状態で保留したまま、それとは別に入力できる機能。

### 「カーソルの側に入力モードを表示」のアイコン表示と使い勝手の改善 ###

現在はテキスト表示ですが、どうせならアイコンを表示して欲しい。

特定のアクションがないと、入力モード表示ウィンドウ?が追従されないので、使い勝手がいまいちです。 これはFirefox側の問題っぽいですが、Firefoxではフォーカス移動のときにも追従してくれない。 直接入力モードでの入力、カーソルの移動やバックスペースのときにも、ちゃんと追従して欲しい。

### アプリケーション内で入力モードを統一 ###

http://lists.sourceforge.jp/mailman/archives/anthy-dev/2005-January/001574.html

### uim-toolbarの表示位置を記憶 ###

http://lists.sourceforge.jp/mailman/archives/anthy-dev/2004-October/001276.html

### uim-cannaのHomeキーで単語登録やメニューを表示 ###

http://lists.sourceforge.jp/mailman/archives/anthy-dev/2006-June/002990.html

### 入力パッドにソフトウェアキーボード的機能の追加 ###

http://lists.sourceforge.jp/mailman/archives/anthy-dev/2006-June/003003.html

### ツール群を一つのプロセスにまとめる ###

http://pc11.2ch.net/test/read.cgi/linux/1135968795/51

```

51 ：login:Penguin：2006/01/22(日) 19:10:59 ID:oQO3Wm5n
    gtkのメモリ消費と立ち上げの遅さがどうにもならないのなら、
    uim-toolbar-*,uim-i m-switcher-gtk,uim-pref-gtk,uim-input-pad-jaあたりは
    いっそ一つのプロセスに機能をまとめてしまった方が
    gtkのオーバーヘッドを最小限にできて良いのかも。

    input-padなんかソース12kしかないんだし。

```

### uim-skkの註釈の有無で同一候補が表示される件 ###

http://pc11.2ch.net/test/read.cgi/linux/1135968795/64

```

64 ：login:Penguin：2006/02/01(水) 00:27:47 ID:fKYTaHPs
    uim-skk でアノテーションの有無で同一候補が 2回現れるのは直らんかな

```

### uim-anthyで「アメニモマケズ」を変換したら「雨ニモマケズ」となって欲しい ###

http://pc11.2ch.net/test/read.cgi/linux/1135968795/638

```

anthy + カタカナ入力モードで…
アメニモマケズ　-> [変換] -> 雨にもまけず
ちょっと悲しかった

```

http://lists.sourceforge.jp/mailman/archives/anthy-dev/2007-June/003495.html

### uim-skkでプログラム実行変換の実現 ###

http://openlab.ring.gr.jp/skk/skk-manual/skk-manual-ja_5.html#SEC86

```

辞書の候補に Emacs Lisp のプログラムが書いてあれば、
そのプログラムを Emacs に実行させ、返り値をカレントバッファに挿入します。
これを 「プログラム実行変換」と読んでいます。例えば、辞書に

 now /(current-time-string)/

というエントリがあるとします。
このとき / n o w SPC と入力すれば、
現在のバッファに current-time-string の返り値である

 Sun Jul 21 06:40:34 1996

のような文字列が挿入されます。

```

もしくは候補に出さない。

http://lists.sourceforge.jp/mailman/archives/anthy-dev/2003-November/000302.html

### デュアルモニタでuim-ximを使うと変換候補が表示されない ###

http://pc11.2ch.net/test/read.cgi/linux/1135968795/809

```

Xを dual monitorで使っているとする。ただし Xinerama は
off にして、:0.0 と :0.1 の2スクリーンで使っているとする。
このとき スクリーン :0.1 に表示した rxvt で漢字変換をしよう
とすると変換中の文字列部分が真っ白になってしまう。

なお
・スクリーン :0.0 での漢字変換は正常である。
・スクリーン :0.1 でも、ターミナル・アプリが gnome-terminal や
Xfce4 のTerminalなら正常である。また firefox でも正常だった。

```

### uim-fepとuim-colorの同期 ###

uim-fepは-Cオプションで配色を指定できますが、可能な範囲でuim-colorに沿った配色になってくれたらうれしい。

http://lists.sourceforge.jp/mailman/archives/anthy-dev/2006-August/003112.html

### キーボードマクロ ###

http://lists.sourceforge.jp/mailman/archives/anthy-dev/2005-November/002627.html

### uim-fepで候補のインライン表示 ###

### uim-skkの個人辞書のソート ###

個人辞書をddskkと同じように"okuri-ari entries."、"okuri-nasi entries."等でソートしてから書き出してほしいです。

### 異なるブリッジ間でuim-skk個人辞書を即座に同期 ###

http://pc11.2ch.net/test/read.cgi/linux/1200850880/45

```

uim-skkを使っているのですが、
GTK_IM_MODULE、QT_IM_MODULE、mltermのuim入力と、
それぞれで変換候補の履歴？が反映されません。
つまりGTKアプリで「夕子」と入力して確定した後、
mltermで「ゆうこ」で変換すると「夕子」が一番先に来ず、他の候補（例えば友子）が一番先に来る、といった具合です。
これは何か直す方法はあるのでしょうか？

```

### uim-dict-gtkのsj3辞書サポート ###

http://pc11.2ch.net/test/read.cgi/linux/1200850880/56

```

uim-dict-gtkはsj3辞書には対応するのかな。

```

### Firefoxの強制確定処理がうまく機能せずダブって表示される ###

http://bugzilla.mozilla.gr.jp/show_bug.cgi?id=5724

```

エディタで未確定文字がある状態でクリックすると、強制確定処理が走ります。
この時にgtk_im_context_resetでIMから未確定文字を破棄するので、次の入力が新規の未
確定文字列を作り始めます。

つまり、
1. なんらかの文字列を入力
2. クリックして強制確定
3. なんらかの文字列を入力

で、3で入力通りに文字列を表示されたら正常です。もし、1で入力した未確定文字列がダ
ブって表示されるようなら、破棄させるのに失敗しています。

```

### uim-ximでuim-candwin-**が見つからないときは自動的に候補ウィンドウ機能を無効に ###**

\**-use-candidate-windowとか**-candidate-op-countを上書き? 変換候補が見えなくならないように。

### [nicolaキーボード](http://nicola.sunicom.co.jp/index.html)（いわゆる親指シフト）への対応． ###

同時打鍵をサポートするためには，キーイベントのタイムスタンプが必要とのこと．API まわりからの変更が必要？


---


タイムスタンプよりタイマが欲しいです。実装しようとおもっていろいろしらべている途中なのですが、ualarmとかで書いても問題ないのでしょうか。ライブラリとして提供されているのでsignalはやばいかなぁと思いつつも、よい手が思い付きません。-- ねる


---


ualarmはまずいです。タイマが必要ならなんらかの形で実装したいと 思います。-- tkng


---


[ComposerFramework](ComposerFramework.md)で対応予定。