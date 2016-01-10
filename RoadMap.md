= 開発スケジュール =



## [Development reformation: Project priorities](http://lists.freedesktop.org/archives/uim/2005-November/001385.html) ##

開発方式の改革に関する二つ目の文章を示したいと思う。

検討すべき議論がなければ、uimの開発を下に列記した優先順位に基づいて行っていきたいと私は考えている。意見があれば挙げてほしい。

技術的側面:

  1. IMツールキットとして柔軟性のある開発プラットフォームとしての地位を築く
  1. ツールキットに基づくマニアックなIMを開発できるようにすること
  1. 通常のIMが要求するであろう機能を開発すること
  1. Unixデスクトップにおけるユーザ指向で使えるIM環境を練り上げる
  1. 他のプラットフォーム（端末、Emacs, Mac OS Xなど）においても同様にユーザ指向で使えるIM環境を練り上げる
  1. 組み込み環境（PDA、携帯電話など）における使えるIM環境を探索する

政治的側面:

  1. YamaKenの意見
  1. 開発者自身のモチベーション・計画・センス
  1. 積極的に参加してくれる人たちからの提案、要求など
  1. コミュニティの役割、我々の考える義務
  1. 常識に基づく「uimは〜であるべき」に対する受け止め方
  1. uimの外部からの「uimは〜であるべき」に対する受け止め方

系統的側面:

  1. 責任の分離
  1. 責任の一体化
  1. 熟慮された名付け
  1. 仕上げのよい部分実装
  1. 効率のよい考察
  1. 迅速な開発

上に述べてきたことはそれほど厳しく適用されないだろうし、これからも優先順位が低いことにもよく取り組むだろう。しかし、上に述べた利点やポリシーがもう一方と一度でも競合してしまうと、たとえ一方が満たされないとしても、優先順位の高いものが優先することとなる。

横柄に見えてしまうかもしれない。しかし、妥協してしまえばどんな目的であれ無駄なものができあがってしまう。私は(おそらく他の人も同様に)オープンな開発現場でのこの初めての苦い経験からそれを知っている。事実、私は過去の妥協により矛盾した人格と私自身の不満を作り上げてしまった。私が考えているuimがuimたらんとすることに対して開発リソースを集中させるために上に述べたことを定義したのだ。優先順位は私がuimが価値のあるものになるために最も早く到達すると信じる順番で記載されている。

「IMツールキット」のようないくつかの用語はまだ十分に説明されていない。この続きとなる(将来の方向性と技術的考察について書いた)文章が送信されるのを待ってほしい。

## uim 1.5.0 ##

内部構造をシンプルにすることを目的としてリリースするものであり、ユーザーが見える部分での変更はほとんどない。

uimのC実装部が複雑になっていることにより、拡張、デザインの改善、入力システムの自動テストを行う上での障害となっているが、これをSchemeに置き換えたり、シンプルにする予定である。

### TODO list ###

[uim 1.5.0 TODO list (updated)](http://groups.google.com/group/uim-en/t/4943747b56f242b4)と[uim 1.5.0 TODOs (mainly Japanese-related issues)](http://groups.google.com/group/uim-ja/t/ef13c6ce25707db)より転載。

今月いっぱいでuim 1.5.0に対してtrunkに実装する機能をfreezeしたいと思っている。1.5.0には以下のような問題点があるのではないかと懸念している。もし以下の内容に付け加える部分があるのであれば是非とも教えてください。

  * libuimでの例外によるエラー処理を加える
    * エラー処理事態は実装されており、コアuim APIへの導入は完了している。しかし、uim-{ipc,helper**}.cやIMプラグインには導入されていない。
  * ログ関数を追加する(fprintf()の置き換え)
  * uim-scmの不正なオブジェクトポインタに対する処理を追加する
    * この機能自体は実装されているが、プラグインではまだ使用されていない
  * バグ修正(パッチ歓迎)
    * uim-shがマルチバイト文字列を評価しようとするとエラーが発生する
      * http://pc11.2ch.net/test/read.cgi/linux/1135968795/785n
    * uim-module-managerの実行に失敗したときに"Success:"と誤って表示される
      * http://lists.freedesktop.org/archives/uim/2007-January/001747.html
      * ローマ字変換表の実装に欠けている部分があった([スレッド 7](uim.md) 759-761)
      * http://pc11.2ch.net/test/read.cgi/linux/1135968795/759-761n
      * 要追加シーケンスのリストアップ
    * 日本語かなキーボードhackコードをマージする(yusuke)
      * http://lists.freedesktop.org/archives/uim/2007-March/001834.html
      * http://groups.google.com/group/uim-en/t/a266abd1390b9e3f
  * かな入力 hack ([r4891](https://code.google.com/p/uim-doc-ja/source/detail?r=4891), kana\_ROとyen signの区別)
    * http://groups.google.com/group/uim-commit/browse_thread/thread/6c8e79a45e28f547/e07ca83a3cb5f0d6#e07ca83a3cb5f0d6
    * GTK+ブリッジ動作確認
    * 必要ならscm側も変更
    * Qt, XIMにも同等のhackを適用
    * 可能であればuim.elへのかな入力hack追加(見送り)
  * bug #[bts:11966](http://bugs.freedesktop.org/show_bug.cgi?id=11966) Requiring m17n-db installed at build time
    * シェルスクリプトuim-m17nlib-relink-icons.inを作成
  * po/とqt/chardict/po/の更新
  * ドキュメントの更新
  * skk-show-annotation?が#tかつskk-show-candidates-with-okuri?が#tだと 候補表示が崩れる([thread 7 823](uim.md))
    * http://pc11.2ch.net/test/read.cgi/linux/1135968795/823n
  * ~/.uim.d/pluginからプラグインがロードできない? ([thread 7 824](uim.md))
    * http://pc11.2ch.net/test/read.cgi/linux/1135968795/784n
  * IM切り換えが何かおかしいらしい(詳細不明) ([thread 7 825-826](uim.md))
    * http://pc11.2ch.net/test/read.cgi/linux/1135968795/825-826n
    * 何が問題とされているのか確認する
  * [UimFep](UimFep.md)でIM名表示がおかしい([thread 7 827](uim.md))
    * http://pc11.2ch.net/test/read.cgi/linux/1135968795/827n
  * skk-show-cursor-on-preedit?が#fの状態でもカーソルが表示される ([thread 7 828-829](uim.md))
    * http://pc11.2ch.net/test/read.cgi/linux/1135968795/828-829n
  * 入力方式の一時切り換えでuim-el-agentが落ちる
    * http://groups.google.com/group/uim-ja/t/f7fe65ccb73c9404
    * http://bugs.freedesktop.org/show_bug.cgi?id=13622**

そして私はやるつもりはないが、以下の作業が残っている。時間があるなら是非とも取りかかって欲しい。

  * 廃止予定のプロシージャー（deprecated-util.scm参照）をSchemeの標準APIで置き換えること
  * m17lib.c、uim-helper**.c、uim-ipc.c、plugin.cのコードの整理を行うこと**

さらに以下のタスクがuim 1.6またはそれ以降に先送りされた。それは、以下の項目が新たなバグを引き起こす可能性があり、1.5.0で行われた多くのコード整理により引き起こされたバグとの鑑別が難しいためである。

  * それぞれのIMで自前でマルチバイト文字コードを操作することができるようにする（sigscheme-trunkブランチ内にある[multibyte.txt](http://uim.googlecode.com/svn/sigscheme-trunk/doc/multibyte.txt)を参照）
  * 文字列を整数ベースで管理しているのをcharオブジェクトに置換する
  * uimのrecordオブジェクトをvectorで扱うようにする

1.5.0で予定されているその他APIの変更点については[uim:doc/COMPATIBILITY](http://uim.googlecode.com/svn/trunk/doc/COMPATIBILITY)を参照のこと。

uim 1.5.0では新たに以下のSchemeの機能が追加される予定である。1.6以降で大改変を行う上で役に立つと思われる。

  * R5RS characters
  * R5RS vectors
  * All of R5RS string procedures
  * R5RS promises (delay and force)
  * SRFI-1 List Library (full featured)
  * SRFI-2 AND-LET**: an AND with local bindings, a guarded LET** special form
  * SRFI-8 receive: Binding to multiple values
  * SRFI-55 require-extension
  * SRFI-95 Sorting and Merging
  * R6RS Unicode characters
  * EUC-JP character codec
  * 'with-char-codec' for dynamic character codec switching
  * 'let-optionals**' for optional argument processing**

さらに1.4に比べ制約が加わることとなるR5RSにあわせる上で以下のようなことが必要となる。

  * SIODバグに起因する互換性を無効にする
  * トップレベルでのルーズなdefineを無効にする

## [API/ABI incompatibility on uim 1.5.0 and future](http://groups.google.com/group/uim-en/t/ea432fe2ffbdc5d2) ##

やあ、開発者のみなさん。

uim 1.5.0で発生するAPI/ABIに互換性が失われること、将来の予測されるであろう変更点について知らせておこうと思う。何かまずいことがあれば教えて欲しい。

[LibUim](LibUim.md) APIの変更に伴うABI非互換については以下のとおり。詳しいことは[uim:doc/COMPATIBILITY](http://uim.googlecode.com/svn/trunk/doc/COMPATIBILITY)を参照して欲しい。

  * http://uim.googlecode.com/svn/trunk/doc/COMPATIBILITY
  * API bug fixes
    * PIDの型を間違っていたのを修正
    * uim\_set\_candidate\_selector\_cb()の戻り値をvoidに変更
  * non-core API removal
    * uim\_symbol\_value\_strを除去
    * uim\_iconv\_openを内部関数に変更
  * incompatible ABI changes
    * UKey\_Shift\_key定数周辺を廃止

「APIバグの修正」は型を誤って定義されたAPIを修正するために必須であるが、APIの呼び出し自体には恐らく影響はないだろう。

「Core APIではない部分の除去」はuim APIを適切に動作させるために行われた。後方互換性を確保するために非推奨API/ABIを残しておくことはできるが、以下の理由で取り除くこととした。

  * [LibUim](LibUim.md) ABIは「APIバグの修正」により既に互換性が失われている。従って、我々にはABIを維持するだけの動機づけを持ち合わせてはいない。
  * [LibUim](LibUim.md)の責任分解点をはっきりさせるためにもAPIの呼び出しをより適切なものに置き換えていく必要性がある。

「ABI互換性のない修正」とは単に定数のリナンバリングのことである。この修正は必要なのないものだが、[LibUim](LibUim.md) ABIが既に「APIバグの修正」によって失われてしまっていることから、リナンバリングするにはちょうど良い時期でもある。

「Core APIではない部分の除去」と「ABI互換性のない修正」に相当するAPI/ABI互換性を保ってほしいということであれば、是非ともその理由を教えて欲しい。

[LibUim](LibUim.md) API/ABIの修正に加えて、uim-scm API/ABIに対しては多くの修正がなされている。

  * incompatible changes on uim-scm API/ABI
    * 「uim 1.5.0で[UIM-SCM uim-scm] APIの再構成を行う」
    * 「uim 1.5.0で[UIM-SCM uim-scm] APIにおける述語論理の再構成を行う」
    * 「uim\_scm\_c\_bool()とuim\_scm\_make\_bool()でのビット長の拡張を行った」

しかし、[UIM-SCM uim-scm] API/ABIはuimの内部インターフェースに準ずる扱いを受けていること、かつ「不安定なインターフェース」であるとみなされていることから、私はこれらの部分を修正することをためらうことはない。

さらに、[LibUim](LibUim.md)のバージョン番号を[uim-scm](UimScm.md) ABIの変更により更新することのないように、uim 1.5.0では[LibUim](LibUim.md)からuim-scm APIをlibuim-scmライブラリとして分離する予定である。

libuim-scmライブラリとして分離された後、uim 2.0までに行う予定であるAPI/ABIの変更として以下のようなものを考えている。

  * uim 2.0ではlibuim-scm API/ABIの修正は行わない
  * uim 2.0までにlibuim API/ABIの修正を段階的に行うか、uim 2.0の時点で一度に行ってしまう。
    * uim\_ipc**_()(実際にはpopen(3)と同等のユーティリティとして実装されているので誤った名称であるが)を除去し、Schemeのユーティリティプロシージャーに変更する
    * Helperプロトコルと文字列ベースの「プロパティAPI」をよりCインターフェースライクな「モードAPI」に置換する
  * uim-helperのコマンド群とuim\_helper_**()を[LibUim](LibUim.md)から分離する。UNIX desktopでは[D-Bus](http://dbus.freedesktop.org/)のようなブリッジ依存のIPCに置き換え、[Qtopia](http://trolltech.com/products/qtopia)ではIPC自体を使わない。
    * im-switcher APIを「プロパティAPI」の後継に置き換える
    * uim 2.0ではuim API全体の改訂を行う

以上述べてきたことについて何か意見があるばあいは教えて欲しい。もし、誰も反対しないのであれば、uim 2.0は以下のような形に再構成されることになるであろう。しかし、[LibUim](LibUim.md)の互換性レイヤーを維持することは非常に手間のかかることなので、全てのブリッジをlibuim2ベースのものに書き換えて古いインターフェースを破棄する戦略をとりたい。たとえ全てのブリッジが新しいインターフェースに書き換えられたとしても[LibUim](LibUim.md)の互換性を維持してほしいという理由があるのであれば教えて欲しい。

```
uim 1.5:
+-------------------------+
|         bridges         |
+-------------------------+
|  libuim  :  uim-helper  | <--> uim-helper-server
+----------+--------------+
```

```
uim 2.0:
+------------------------+
|       new bridges      |
+-----------+--+---------+----------------------+
|  libuim2  |  |  bridge-dependent IPC (D-Bus)  | <--> a msg bus for uim
+-----------+  +--------------------------------+
```

```
uim 2.0 (legacy interface):
+----------------------------------+
|  legacy bridges with uim-helper  |
+----------------------------------+
|   libuim (compatibility layer)   | <--> uim-helper-server
+----------------------------------+
|             libuim2              |
+----------------------------------+
```

## uim 1.6.0 and later ##

uim 1.6.0では広範囲にわたる再編成を行う。ユーザに見える形での変更点も多くなるだろう。

uim 1.7.0では広範囲にわたる再編成を行う。ユーザに見える形での変更点も多くなるだろう。
IMの開発を広範囲に行うために[ComposerFramework](ComposerFramework.md)が導入される予定となっている。

  * http://groups.google.com/group/uim-en/t/127a17dbaf4da9af
  * http://groups.google.com/group/uim-ja/t/0543bdf1c18f1bbf

## uim 2.0.0 ##

全面的なuim APIが改訂されるでしょう。

## Other topics related to uim development ##

### API for input mode -specified text field ###

I prefer using generic action API for such purpose instead of adding a dedicated API for it.

  * http://bugzilla.gnome.org/show_bug.cgi?id=346780
  * http://lists.sourceforge.jp/mailman/archives/scim-imengine-dev/2006-November/001412.html (Japanese)

### IMBUS ###

SCIMとIIIMFの共通のフロントエンドとなる入力システムの仲介システムについて現在議論されている。しかしながら、uimは以下の理由によりこの議論には参加しない。

  * 開発の方向性、（短期的）目標がuimのプロジェクトの方針と異なるため
  * 単に参加するために十分な時間を割くことができないため

為すべきことはリリースを待つことと、uimにとってどのようなメリットがあるのかを評価することである。

  * http://www.freedesktop.org/wiki/Software/imbus
  * http://www.nabble.com/Question-regarding-the-status-of-the-next-version-of-SCIM-t2564335s16577.html
  * http://code.google.com/p/imbus/

### m17nライブラリに対応した[UimPref](UimPref.md)フロントエンド ###

m17nライブラリに対する設定スキームとuimへの実装が現在議論されているところである。

  * http://lists.sourceforge.jp/mailman/archives/anthy-dev/2006-August/003140.html (Japanese)
  * http://lists.sourceforge.jp/mailman/archives/anthy-dev/2006-September/003150.html (Japanese)
  * http://lists.sourceforge.jp/mailman/archives/anthy-dev/2006-September/003151.html (Japanese)
  * http://lists.sourceforge.jp/mailman/archives/anthy-dev/2006-November/003208.html (Japanese)

### 分節ベースの中国語入力システムを実装してほしいとの要望について ###

分節ベースの入力システムであるFcitxをuimに移植するように中国人ユーザから提案があった。しかし、XIMに依存していることから技術的に容易ではないため、uim-fcitxは実装されないであろう。

  * http://lists.freedesktop.org/archives/uim/2006-October/001584.html
  * http://lists.freedesktop.org/archives/uim/2006-November/001604.html
  * http://lists.freedesktop.org/archives/uim/2006-November/001617.html
  * http://lists.sourceforge.jp/mailman/archives/anthy-dev/2005-June/002079.html (Japanese)

## 他 ##

  * [New scm for zh\_CN](http://groups.google.com/group/uim-en/t/dd0079d1fad07986)
  * [API Documentation](http://groups.google.com/group/uim-ja/t/53909274c993b70a)
  * [Fast lookup of Korean-Chinese dictionary](http://groups.google.com/group/uim-en/browse_thread/thread/782b81fb23636330)

## ブロッカーバグ ##

  * [uim 1.6.0 is not released yet](http://bugs.freedesktop.org/show_bug.cgi?id=7730)
  * [uim 2.0.0 is not released yet](http://bugs.freedesktop.org/show_bug.cgi?id=9643)
