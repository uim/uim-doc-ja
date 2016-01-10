= コミットポリシー =

http://lists.sourceforge.jp/mailman/archives/anthy-dev/2005-September/002377.html

http://lists.sourceforge.jp/mailman/archives/anthy-dev/2005-October/002503.html

http://groups.google.com/group/uim-ja/t/e0616ddc710efbea



## コミットする単位に関して ##

コミットするのは一まとまりの単位毎にしましょう。 何をもって一まとまりとするか、というのは難しい問題ですが、現状では、複数の機能改善等が一度にコミットされるケースが散見されます。 これは以下の点で問題です。

  * revertしにくい
  * コードを読んで把握しにくい

コミット単位が小さくすると今度は動かないrevisionが出てくるよ問題が発生するものと思われますが、とりあえずは現状を改善するために、コミット単位は小さくしていきましょう。 合言葉は「迷ったらこまめにコミット」で。

特に、バグフィックスと機能追加はできるだけ混ぜないようにしましょう。 同じ箇所に対する変更であっても、一端バグを修正して、それから機能を追加するようにしましょう。 これは、バグ修正を安定版ブランチへ適用する事が目的です。 （ただし、「書き換えたらバグがなくなってしまった」というような場合は除きます。 このような場合は、深刻なバグであれば、別途0.4ブランチで修正するしかないでしょう。）

## コミットの種類に関して ##

コミットによりリポジトリに加えられる変更には、さまざまなものがありますが、ここではおおざっぱに以下のようにわけてみます。

  * (a)バグ修正
  * (b)機能改善（小）
  * (c)機能改善（大）

バグ修正は字面の通り、バグ修正です。 機能追加（小）は、小さいコードの変更量で新しい機能を追加したり、既存の機能を改善したりするものです。 目安としてはdiffが30行以内、ぐらいを想定しています。 このような分類を作った目的は、「この変更はどのブランチにコミットするべきか？」というのを簡便に判定することです。

30行以内(unified diffですよね?)では本当に些細な修正しかできないので実態に合わないと思いますが、変更の大きさに客観的基準を設ける事には賛成です。

trunk:: 通常は制限なし。リリース三日前ぐらいからはcは行わない。0.6が近付いたら状況は変わるかも。

本来ならcode freezeと共にそのバージョン専用のリリースブランチを作成してtrunkは自由にしておくべきだと思いますが、とりあえずは了解です。

0.4:: a, bのみ。bを行うかどうかは各コミッタで判断。bの判断規準は「迷ったらコミットするな。」逆に、trunkにコミットしたバグ修正は、問題なく適用できる限り0.4にもコミットすること。

了解です。 ただし、API/ABIの変更があった場合には[uim:doc/COMPATIBILITY](http://uim.googlecode.com/svn/trunk/doc/COMPATIBILITY)に記述する事にしましょう。また、ABIの変更(例: [r1309](http://websvn.freedesktop.org/uim?view=rev&revision=1309))は原則として避けるべきです。 たとえそのAPIが使われてなかったとしても。

r5rs:: 制限なし。trunkへのマージが近付いたらしばらくはバグ修正とtrunkからの同期作業のみ。マージ時期に関しては別途告知を出すこと。branches:: tags::

## trunkとr5rsの同期に関して ##

r5rsブランチでsvk pullを行うと、自動でtrunkでの変更をr5rsブランチに追加してくれます。 というわけで、基本的には手作業でr5rsブランチにtrunkでのコミットを適用する必要はありません。 1週間に1度、もしくはそれ以上の頻度を目安にマージを行うこと。

完全に自動的には同期できない事を前提に続けましょう。

## ファイルの追加に関して ##

ファイルを追加した場合、Makefile.amに適切な記述を追加することを忘れると、ビルドできなかったり、動かない原因になります。 単純な場合に関してはmake releasetestによるテストで回避できますが、以下の場合に関しては特に気を付けて回避しなければなりません。

  * Schemeのファイルを追加した場合
  * デフォルトでconfigureオプションがオフの場合

前者はSchemeのテストコードを追加する事で回避できるでしょう。

後者はmake releasetestのルールを変更しないと回避できません。 configureオプションを追加した場合は、make releasetestをいじる必要がないかどうか、確認しましょう。

## テストに関して ##

テストに関してはいろいろ改善したいところがあるのですが、とりあえず将来的には「コミット前に関連テストにパスすることを確認すること」というポリシーを入れたい、というのが希望です。

commit毎に必ずテストというのはコストが非現実的なので受け入れ難いです。 連続した5回のcommitで1つの目的を達成する場合もあるわけで、そのような場合には最後にテストすればOKでしょう。 もちろんサッと終わる自動テストが対象コードに用意されてるならそれを走らせるぐらいは推奨していいでしょうが。

あまりキツいルールを課すとかえって守られなくなります。

## コミット前の作業に関して ##

svn diffで、コミット前に変更点をもう一度確認しましょう。

## コミットログに関して ##

コミットログにはそのコミットの目的を書きましょう。 目的が書けないようなコミットは行うべきではありません。 もしくは、目的の分類が不十分です。目的は以下のようなものに分類されます。 （ここに無いものがあれば追加してください。）

  * cosmetic change,
  * bug fix,
  * new feature,
  * refactoring

documentationを追加しましょう。 あと"bug fix"は複合語として"bugfix"にした方が扱いやすいように思います。 好みですが。

それから、[**new feature**]のような形式で重要性を示すのはどうでしょう? 前回リリースからの差を確認したり、少ない時間で開発を追うのに便利だと思います。 [ChangeLog](http://en.wikipedia.org/wiki/Changelog)生成時にはこの重要な変更のみを含めるようにした方がいいかもしれません。

あと外部からパッチをもらった場合に[ChangeLog](http://en.wikipedia.org/wiki/Changelog)に本人の名前を残せるように定型文で言及するようにしましょう。

```
[new feature] Patch by HOGE Fugao <hoge at example.com> posted in
[Anthy-dev 65535]. These functions ...

    ↓

2005-10-08 HOGE Fugao <hoge at example.com>

        [new feature] by the patch posted in [Anthy-dev
        65535]. These functions ...
```

コメントやドキュメントの変更はどうしようか迷い中。 以下のような感じで書くことを想定しています。 ログの書式は以下のような感じで考えてます。

```
[bug fix] Fixed a typo.
* uim/uim.c:
 -(uim_init): Replaced 'uiim' with 'uim'.
```

いくつか変えたい点があります。

  * commitのカテゴリ(と要約)の後には空行を挿入すべき
  * 変更内容が自明な場合("[fix](bug.md) Fixed a typo")は要約は積極的に省略し、単に"[fix](bug.md)"とした方がよい

また、uimのcommit logはある程度[ChangeLog](http://en.wikipedia.org/wiki/Changelog)形式に似せてあるのでその慣習に従って以下のようにすべきと思います。

  * "replaced"のように無理に時制を合わせようとせず、単に"replace" とする
  * "uim.c: (uim-init):"のように関数名等がリストされている場合はファイル名の直後にはコロンを付けず"uim.c (uim-init):"とする

http://www.gnu.org/prep/standards/standards.html#Style-of-Change-Logs

テキスト整形ルールについては以下の3つが候補になるかと思います。 徳永さんの形式は[ChangeLog](http://en.wikipedia.org/wiki/Changelog)としても一般的なitemized listとしても中途半端なので見る人にメリットが無いと思います。

私は3番目のitemized形式が見やすいと思いますが、意見が割れるようなら標準であるという事で1番目の[ChangeLog](http://en.wikipedia.org/wiki/Changelog)風にしましょう。 font-lockすればまあそれなりに見れますし。

```
ほぼChangeLog風:
----------------------------------------------------------------
[bugfix] This explanation is explanation for explanation so
don't mind this.

* uim/uim.c (uim_init, uim_create_context, get_context_id)
(uim_reset_context): Fix a typo 'uiim' with 'uim'.
(uim_quit): Fix incorrect function definition. This explanation
is explanation for explanation so don't mind this.
----------------------------------------------------------------

indented:
----------------------------------------------------------------
[bugfix] This explanation is explanation for explanation so
don't mind this.

* uim/uim.c
  (uim_init, uim_create_context, get_context_id,
  uim_reset_context): Fix a typo 'uiim' with 'uim'.
  (uim_quit): Fix incorrect function definition. This
  explanation is explanation for explanation so don't mind this.
----------------------------------------------------------------

itemized:
----------------------------------------------------------------
[bugfix] This explanation is explanation for explanation so
don't mind this.

* uim/uim.c
  - (uim_init, uim_create_context, get_context_id,
    uim_reset_context): Fix a typo 'uiim' with 'uim'.
  - (uim_quit): Fix incorrect function definition. This
    explanation is explanation for explanation so don't mind
    this.
----------------------------------------------------------------
```

http://slashdot.jp/~YamaKenZ/journal/314487

複数の事項は複数に分けてcommitする:: 例えば、見た目の変更と論理の変更は分けた方がよい。他人が変更の妥当性を確認したり、誰によらず後からコード仕様の変化を追ったりする場合、余計なdiffを見なくて済むようになる。また、論理の修正も関連する変更毎に分けてcommitする。こうする事で関心のあるファイルや関数に変更のあったrevisionのみを低コストで確認できるし、問題のあった場合に機能単位でrevertできる。どの関数を触ったかlogに残す:: 論理の変更(リファクタリングも含む)を行った関数については、最低でも関数名をcommit logに残す。その関数に関心のある人が変更を確認したり、後からデバッグする際に問題のありそうなrevisionを確認するのを可能にするため。見た目の変更は無理に関数名毎の記録を残さなくても問題ない。commit前にdiffを一通り頭から眺める:: 論理も軽く再確認するのが望ましいが、ざっと流し読みするだけでも、意図していないおかしな変化を検出できる(おかしなfile property、行末のwhitespace付加等)。

## inputmethod-icons ##

http://lists.freedesktop.org/archives/uim/2006-December/001654.html

I saw that you had added an icon for it. But since [uim:pixmaps/](http://uim.googlecode.com/svn/trunk/pixmaps/) directory is intended to be synchronized with the [inputmethod-icons](http://code.google.com/p/inputmethod-icons/) package, please commit all changes to the inputmethod-icons repository first, and then import from it even if such a trivial changes.

What I worried about is that complicated tracking of original source and change histories. Making the inputmethod-icons repository primary source (ja: ichigen-ka) simplifies the tracking problem. Please consider it.

## 他のプロジェクトから持って来たコード ##

http://lists.sourceforge.jp/mailman/archives/anthy-dev/2006-June/002980.html

他のプロジェクトから持って来た各コードですが、以下の情報の提供を お願いします。できれば直接各ファイルにライセンスと一緒に挿入して 欲しいところですが、このメールへの返信で構いません。

  * コピー元のGauche, Biglooのバージョン
  * コピーした日付
  * ファイル名は一対一にコピー元と対応しているのかどうか
  * 追加、削除、変更の有無

http://lists.freedesktop.org/archives/uim/2005-September/001344.html http://utyuuzin.net/d/?year=2005;month=3Q;category=uim

quick hackでuimやximの下に分散していたのをreplaceの下にまとめるためのpatch. ソースのoriginや責任分界点をはっきりさせるのが目的。

これをcommitすると激しく混乱を生じさせることになりかねないのでとりあえずpatchで打ち止め。 あと、ximは管轄外なのでpendingにしてとりあえずuimの下だけの分離で止めてあります。

http://slashdot.jp/~YamaKenZ/journal/389088

ところで、このopenbsd-compatにはuimでも使ってるBSD由来の代替関数がいい具合に揃っていて更新を追うのが楽になりそうなんで、サクっとuimのvendorブランチに取り込んでおきました。ポータビリティの低い関数を使いたい場合は、まずここから代替実装を探すようにお願いします >committer各位
