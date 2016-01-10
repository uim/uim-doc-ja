= uim-tutcode =



## これは何？ ##

[TUT-Code](http://www.crew.sfc.keio.ac.jp/~chk/index-old.html)入力方式のuim版。

## 使い方 ##

  1. あらかじめ[tc2などに含まれている交ぜ書き辞書](http://openlab.ring.gr.jp/tcode/soft.html)などを入手しておいてください。交ぜ書き変換に必要ですが、これはuimに含まれていません。
  1. [UimPref](UimPref.md)を起動してください。
    * [UimToolbar](UimToolbar.md)の設定アイコンをクリック
    * ターミナルエミュレータなどでuim-pref-gtk(もしくはuim-pref-qt4かuim-pref-qt)を実行
  1. 「TUT-Code」→「TUT-Code 辞書」→「交ぜ書き変換辞書ファイル」の「選択...」ボタンを押して、辞書ファイルを指定します。
  1. [UimImSwitcher](UimImSwitcher.md)や[UimToolbar](UimToolbar.md)からTUT-Codeに切り換えてください。
    1. TUT-Codeが見つからない場合は[UimPref](UimPref.md)を起動してください。
    1. 起動したら、「全体設定」→「入力方式の利用準備」→「使用可能にする入力方式」の「編集...」ボタンを押して、左の有効アイテムにTUT-Codeを追加してください。
      * そこにもTUT-Codeが見つからない場合、uim-tutcodeはインストールされていないのかもしれません。確認してみてください。
    1. 追加が完了したら、TUT-Codeで入力したいアプリケーションを再起動してください。
  1. [UimImSwitcher](UimImSwitcher.md)や[UimToolbar](UimToolbar.md)による切り換えは一時的なものです。永続的な変更を望むなら[UimPref](UimPref.md)で設定する必要があります。
  1. [UimPref](UimPref.md)を起動したら、「全体設定」→「入力方式の利用準備」→「標準の入力方式を指定」のチェックボックスにチェックを入れます。
  1. そのすぐ下の「標準の入力方式」に、TUT-Codeをセットしてください。

### サポートしている入力モード ###

  * 直接入力モード
  * ひらがなモード
  * カタカナモード
  * 記号入力モード
  * 2ストローク記号入力モード

### 標準で指定されているキー設定 ###

| 動作 | キー |
|:---|:---|
| オン/オフ | 全角/半角、Shift+Space、Ctrl+\ |
| ひらがな/カタカナ入力モードを反転移行 | '  |
| 記号入力モードを反転 | Ctrl+`_` |
| 交ぜ書き変換 | alj |
| 部首合成変換 | ala |
| 英字変換(SKK abbrev) | al/ |
| 仮想鍵盤ウィンドウの表示を反転 | Ctrl+/ |
| 補完開始 | Ctrl+. |
| 変換開始 | Space |
| 次の変換候補へ移動 | Space、↓、Ctrl+n |
| 前の変換候補へ移動 | ↑、Ctrl+p |
| 候補ウィンドウを次のページへ移動 | PgDn |
| 候補ウィンドウを次のページへ移動 | PgUp |
| 変換確定 | Return、Ctrl+m、Ctrl+j |
| キャンセル | Esc、Ctrl+[、Ctrl+g |
| カーソルの左の一字を削除 | BS、Ctrl+h |
| 交ぜ書き変換個人辞書への単語登録 | |  |
| 交ぜ書き変換個人辞書からの単語削除 | !  |
| 交ぜ書き変換で読みを伸ばす | <  |
| 交ぜ書き変換で読みを縮める | >  |
| 入力途中のキーストロークを挿入 | Space |

### T-CodeやTry-Codeとして使う ###

コード表ファイルを変更することで、T-CodeやTry-Codeとして使えます。

  * [UimPref](UimPref.md)で「TUT-Code」→「コード表ファイル」に/usr/local/share/uim/tcode.scm（T-Code）や/usr/local/share/uim/trycode.scm（Try-Code）を指定してください。

  * 「TUT-Code キー設定1」→「交ぜ書き変換モード」に「fj」を、
  * 「部首合成変換モード」に「jf」を、
  * 「英字変換(SKK abbrev)モード」に「47」(fjの2段上)等、コード表で未割当のストロークを指定してください。

  * 「TUT-Code キー設定1」→「ひらがな/カタカナ入力モードを反転」を空にしてください。

### vi協調モード ###

vi（クローン）でコマンドモードに戻る時、uimを直接入力モードに戻すことができます。

[UimPref](UimPref.md)で「TUT-Code」→「vi協調モードを有効にする」のチェックボックスにチェックを入れてください。

標準のキー設定は以下のようになっています。

| 動作 | キー |
|:---|:---|
| vi協調モードでESCとして扱うキー | ESC、Ctrl+[ |

### Dvorakキーボード ###

Dvorak配列のキーボード用にコード表を補正します。

[UimPref](UimPref.md)で「TUT-Code」→「Dvorakキーボードを使用する」のチェックボックスにチェックを入れてください。

「表形式の候補ウィンドウのキー配列」として「dvorak」を選んでください。

## 部首合成変換 ##

再帰的な部首合成変換も可能です。
部首合成のアルゴリズムは以下の3つから選択可能です。
  * tc-2.1+[tcode-ml:1925]
  * 漢直Win YAMANOBE
  * tc-2.3.1-22.6 (対話的な部首合成変換と同じ処理を使用するので、[bushu.index2とbushu.expandファイル](http://www1.interq.or.jp/~deton/tutcode/#bushudic)の設定が必要)

### 対話的な部首合成変換 ###

tc-2.3.1のtc-bushu.elの移植です(ただしsortでの打ちやすさの考慮は未対応)。

「対話的な部首合成変換を有効にする」
「bushu.index2ファイル」「bushu.expandファイル」を設定し、
キー設定で「対話的な部首合成変換モード」を設定すると使用可能になります。
[bushu.index2とbushu.expandファイル](http://www1.interq.or.jp/~deton/tutcode/#bushudic)は、
tc-2.3.1のインストール時に生成・インストールされるファイルです。

対話的な部首合成変換時の候補ウィンドウ:

![http://uim-doc-ja.googlecode.com/svn/wiki/UimTutcodeInteractiveBushu.png](http://uim-doc-ja.googlecode.com/svn/wiki/UimTutcodeInteractiveBushu.png)

## 交ぜ書き変換 ##

交ぜ書き変換辞書はtc2と同じ形式(SKK辞書と同様の形式)です。

### 交ぜ書き変換辞書 ###

交ぜ書き変換辞書(例:/usr/local/share/tc/mazegaki.dic)へのアクセスは
libuim-skk.soの機能を使っています。
そのため、学習機能もSKKと同様の動作になります:

  * 確定した候補は次回の変換から先頭に来ます。tc2と同様に、先頭数個の候補順を変えたくない場合は、「交ぜ書き変換の学習から除外する候補数」にその個数を設定してください。
  * 確定した候補は個人辞書(~/.mazegaki.dic)に保存されます。

これらの学習機能をオフにするには、
「交ぜ書き変換の学習を有効にする」のチェックを外してください。

交ぜ書き変換辞書への登録・削除もSKKと同様の動作になります:

  * ~/.mazegaki.dicに登録・削除。
  * 登録: 変換候補の最後まで行ったら再帰的登録モードに移行。あるいは、読みを入力後、|を押す。
  * 削除: 辞書からの削除は、削除したい候補を選んで!を押す。

### 活用する語の変換 ###

「交ぜ書き変換での活用する語の変換を有効にする」を設定すると、活用しない語
としての変換候補が見つからなかった時に、活用する語として変換を試みます。
(ただし、活用しない語の候補が1個の場合の自動確定はしなくなります。
次の文字の入力を開始すれば確定されます。)

また、最初から活用する語として変換したい場合は、読みに"―"を付けるか、
「後置型交ぜ書き変換開始 (活用する語) 」キーで変換開始してください。

候補表示中は、<と>キーにより、語幹(活用語尾以外の部分)の伸縮が可能です。
(ただし、読みの入力時に"―"を付けて語幹を明示した場合を除く)

### 読みをカタカナとして確定 ###

「交ぜ書き変換の読みをカタカナとして確定する」キーに
カタカナ確定キーを設定すると使用可能になります。

### 英字変換(SKK abbrev)モード ###

英字変換(SKK abbrev)モードを追加しています(al/)。
例えば、「file」を入力して「ファイル」に変換する機能です。

## 後置型変換 ##

uimのtext acquisition API(surrounding text API)を使って、
カーソル前の文字列の取得・削除を行います。
そのため、uimのtext acquisition APIをサポートしているブリッジ
(uim-gtk, uim-qt3, uim-qt4)でのみ後置型変換が可能です。

これら以外のブリッジでも後置型変換を使いたい場合、
「surrounding text APIの代替方法を有効にする」を設定すると、
surrounding text APIが使用できない場合に、
文字列の取得は内部の確定済文字列バッファから行い、
文字列の削除は"\b"(tutcode-fallback-backspace-string)を送出します。

  * \b(BS,0x08)文字を受けた時に削除を行うアプリでのみ動作。
  * 内部の確定済文字列バッファは補完と兼用で、長さは「補完の際に考慮する文字数の最大値」の値。

### 後置型部首合成変換 ###

後置型部首合成変換は、
「後置型部首合成変換」キーを設定すると使用可能になります。

### 後置型交ぜ書き変換 ###

後置型交ぜ書き変換は、以下の開始キーを設定すると使用可能になります。

| 後置型交ぜ書き変換開始 (活用しない語) |
|:---------------------|
| 後置型交ぜ書き変換開始 (活用する語)  |
| 後置型交ぜ書き変換開始 (読み1文字)  |
| ...                  |
| 後置型交ぜ書き変換開始 (読み9文字)  |
| 後置型交ぜ書き変換開始 (活用する語,読み1文字) |
| ...                  |
| 後置型交ぜ書き変換開始 (活用する語,読み9文字) |

#### 後置型交ぜ書き変換における、読み/語幹の伸縮 ####

候補表示中は、<と>キーにより、読み/語幹の伸縮が可能です。
活用する語に関しては、語幹が長いものを優先して変換します。

例:

> 「あおい」>「おい」>「い」
> > (「交ぜ書き変換での活用する語の変換を有効にする」が設定されている場合、
> > さらに縮めると活用する語として変換)
> > > >「あおい―」>「あお―」>「おい―」>「あ―」>「お―」>「い―」

> > (実際にはtc2付属のmazegaki.dicに「あおい―」は無いのでスキップ)

読みの文字数を指定して変換開始した場合、
活用する語に関しては、読みは指定された文字数で固定して語幹のみ伸縮。

例(「あおい」に対して3文字指定):「あおい―」>「あお―」>「あ―」

### 後置型カタカナ変換 ###

後置型カタカナ変換は、以下の4種類があります。

  * 対象の文字数を指定: カタカナに変換する文字数を指定します。
  * 対象伸縮モード開始: カタカナ変換対象の文字列を選択するモードを開始します(<と>キーにより、字数の伸縮が可能です。後置型交ぜ書き変換同様)。
  * ひらがなが続く間: ひらがなや「ー」が続く間、カタカナ変換対象にします。
  * ひらがなとして残す文字数を指定: ひらがなや「ー」が続く間カタカナ変換対象にしますが、指定された文字数はカタカナに変換しないでひらがなとして残します。カタカナに変換する文字列が長くて文字数を数えるのが面倒な場合向けです。
    * 例:「例えばあぷりけーしょん」→(2文字を残して変換)→「例えばアプリケーション」

また、後置型のカタカナ変換を行った直後であれば、カタカナ文字列を縮めることも可能です。
繰り返し実行可能です。
  * 例:「例えばあぷりけーしょん」→(ひらがなが続く間変換)→「例エバアプリケーション」→(1文字縮める)→「例えバアプリケーション」→(1文字縮める)→「例エバアプリケーション」

後置型カタカナ変換は、以下の開始キーを設定すると使用可能になります。

| 後置型カタカナ変換 (対象伸縮モード) | カタカナ変換対象の文字列を選択するモードを開始(後置型交ぜ書き変換同様) |
|:--------------------|:-------------------------------------|
| 後置型カタカナ変換 (ひらがなが続く間) | ひらがなや「ー」が続く間対象文字列として、カタカナに置換         |
| 後置型カタカナ変換 (1文字)     | 指定文字列をカタカナに置換                        |
| ...                 | 指定文字列をカタカナに置換                        |
| 後置型カタカナ変換 (9文字)     | 指定文字列をカタカナに置換                        |
| 後置型カタカナ変換 (1文字除く)   | 指定文字列をひらがなとして残してカタカナに置換              |
| ...                 | 指定文字列をひらがなとして残してカタカナに置換              |
| 後置型カタカナ変換 (6文字除く)   | 指定文字列をひらがなとして残してカタカナに置換              |
| 後置型カタカナ変換 (1文字縮め)   | 直前の後置型カタカナ変換を指定文字数縮める                |
| ...                 | 直前の後置型カタカナ変換を指定文字数縮める                |
| 後置型カタカナ変換 (6文字縮め)   | 直前の後置型カタカナ変換を指定文字数縮める                |

### 後置型漢字→入力シーケンス変換 ###

TUT-Codeオン・オフのモード切り替えなしで英単語を入力して、
後から英字化するための機能です。
「漢字に対応しないキーシーケンスを残す」を設定した上で、
英単語入力後に、tutcode-verbose-stroke-key(デフォルトはスペースキー)を
打鍵することでシーケンスを終端した後に、以下の開始キーを入力して下さい。
(変換後に、最後のtutcode-verbose-stroke-keyは自動削除します)

例:"undo "と打鍵すると"趣・"と表示され、以下の開始キーで、"undo"に変換。

| 後置型漢字→シーケンス変換開始 |
|:----------------|
| 後置型漢字→シーケンス変換 (1文字) |
| ...             |
| 後置型漢字→シーケンス変換 (9文字) |

文字数を指定しない場合、<と>キーにより、字数の伸縮が可能です。
文字数を指定しない場合、英単語入力前にスペースを入力しておくと、
スペースより後の文字を英字に変換します。
このとき、英単語の区切りのために入力したスペースを自動削除するには、
「後置型漢字→シーケンス変換時に直前の区切り文字を削除する」を設定してください。

例:" code "と打鍵すると" 演各 "と表示され、開始キーで、"code"に変換。

注:英単語中に前置型交ぜ書き変換開始などの機能に対するシーケンスが
含まれていると、該当する機能が実行されてしまいます。
現状では、それらの機能に対するシーケンスを、
英単語中では出現しないシーケンスに変更することで回避してください。

例:"/local/"と打つと"授阪"の後に"al/"により前置型英字変換モードが開始
(なお、"local/"の場合は"薬児適"なので問題なし)

### 後置型入力シーケンス→漢字変換 ###

TUT-Codeオンにし忘れてTUT-Codeを入力した場合に後から漢字に変換するための
機能です。

| 後置型シーケンス→漢字変換開始 |
|:----------------|
| 後置型シーケンス→漢字変換 (1文字) |
| ...             |
| 後置型シーケンス→漢字変換 (9文字) |

前置型交ぜ書き変換の読み入力など、確定されていない入力は消えます。

例:"aljekri"を変換→""。"ekri"だけ変換→"かい"。
"aljekri \n"のように確定されている場合→"下位"

## selectionに対する変換 ##

uimのtext acquisition API(surrounding text API)を使って、
selection文字列の取得・削除を行います。

| セレクションを交ぜ書き変換 |
|:--------------|
| セレクションを交ぜ書き変換 (活用する語) |
| セレクションをカタカナ変換 |
| セレクションを漢字→シーケンス変換 |
| セレクションをシーケンス→漢字変換 |

## ヘルプ機能 ##

### 仮想鍵盤表示 ###

各位置のキーの打鍵により入力される文字を表示します。
「仮想鍵盤ウィンドウを使用する」での表示・非表示設定の他に、
Ctrl+/で一時的に表示・非表示の切り替えも可能です。
(打ち方があやふやな文字を入力するときだけ表示したい場合があるので)

  * 「`*`」前付き文字:該当キーの打鍵により、該当文字を含む仮想鍵盤が表示されることを表します。(中間打鍵)
  * 「+」前付き文字:該当キーが、該当文字の中間打鍵であることを表します。(熟語ガイドの中間打鍵)
  * 「+」後付き文字:熟語ガイドの最終打鍵であることを表します。

ホームポジションで左手人差し指打鍵時に表示される仮想鍵盤:

![http://uim-doc-ja.googlecode.com/svn/wiki/UimTutcodeVirtualKeyboardHelp.png](http://uim-doc-ja.googlecode.com/svn/wiki/UimTutcodeVirtualKeyboardHelp.png)

### 自動ヘルプ表示機能 ###

交ぜ書き変換や部首合成変換で入力した文字の打ち方を表示します。
部首合成方法のヘルプは、bushu.helpファイルが設定されていれば
二分探索して表示します。bushu.help内に見つからない場合でも、
簡単な部首合成に関しては表示可能です。

例:交ぜ書き変換で「憂鬱」を確定した場合の自動ヘルプウィンドウ:

![http://uim-doc-ja.googlecode.com/svn/wiki/UimTutcodeAutoHelp.png](http://uim-doc-ja.googlecode.com/svn/wiki/UimTutcodeAutoHelp.png)

#### 直近に表示した自動ヘルプの再表示 ####

キー設定で「直近の自動ヘルプを表示」を設定すると使用可能になります。

#### 直近に表示した自動ヘルプ内容の確定 ####

キー設定で「直近の自動ヘルプ内容の確定」を設定すると使用可能になります。
候補ウィンドウに表示したヘルプ内容を以下のような文字列にしてcommitします。
(部首合成シーケンス(例:"林缶")をコピーして、後でクリップボードから
前置型部首合成変換のpreeditへペーストして変換したい場合向け)

```
       |  |  |  |  ||            |  |  |     |  ||
       |  |  |  | b||            |  |  |  f  |  ||
       | 3|  |  |  ||            |  |  |1(憂)|  ||
       |  | d|  | e||2a(鬱▲林缶)|  |  |     |  ||
```

#### 文字ヘルプ表示機能 ####

カーソル位置直前の文字のヘルプ(打ち方)を表示します。
(uimのtext acquisition APIを使ってカーソル位置直前の文字を取得)

## 補完/予測入力・熟語ガイド ##

  * 「補完」:確定済文字列に対して、続く文字列の候補を表示します。
  * 「予測入力」:交ぜ書き変換の読みに対して、変換後文字列の候補を表示します。
  * 「熟語ガイド」:補完/予測入力候補文字列をもとに、次に入力が予測される文字の打鍵ガイドを表示します('+'を付けて表示)。

  * 補完/予測入力・熟語ガイドとも候補ウィンドウに表示します。
  * 補完/予測入力機能を使うには、[UimPref](UimPref.md)の「補助予測入力」グループの設定が必要です。
    1. Look-SKKを有効にしてmazegaki.dic相当の辞書ファイルを指定する。(主に予測入力用)
    1. Lookを有効にして単語ファイルを指定する(補完用)。mazegaki.dicの読みに、漢字としては入っていない単語を補完したい場合。(例:「狂」を入力した時点で「奔」を補完して欲しいが、「狂奔」がmazegaki.dicには読みとしては入っていないので、1だけでは補完されない(1は読みを検索するので))。mazegaki.dicから変換後の単語を抜き出して、補完用単語ファイルを生成するには、以下のコマンドで可能。<br><code>awk -F'[ /]' '{for(i=3;i&lt;=NF;i++)if(length($i)&gt;2)print $i}' mazegaki.dic | sort -u &gt; mazegaki.words</code>
<ol><li>Sqlite3を有効にする。補完/予測入力で選択した候補を学習したい場合、一番上に配置。<br>
</li></ol><blockquote>二分探索するので、1,2のファイルはソートしておく必要があります。<br>
</blockquote><ul><li>補完/予測入力の開始は以下のいずれかのタイミング:<br>
<ul><li>補完: tutcodeオンの状態でtutcode-completion-chars-minの文字数入力時<br>
</li><li>補完: tutcodeオンの状態でCtrl+.打鍵時<br>
</li><li>予測入力: 交ぜ書き変換の読み入力状態でtutcode-prediction-start-char-countの文字数入力時<br>
</li><li>予測入力: 交ぜ書き変換の読み入力状態でCtrl+.打鍵時<br>
</li></ul></li><li>補完候補表示にさらにCtrl+.を打鍵すると対象文字を1つ減らして再補完。長すぎる文字列を対象に補完された場合に、補完し直しができるように。<br>
</li><li>上記の補完開始文字数(tutcode-completion-chars-min)や予測開始文字数(tutcode-prediction-start-char-count)を0に設定すると、Ctrl+.打鍵時にのみ補完/予測入力候補を表示します。<br>
</li><li>熟語ガイド(次に入力が予測される文字の打鍵ガイド)は補完/予測入力候補から作っています。<br>
</li><li>仮想鍵盤上での熟語ガイド表示<br>
<ul><li>熟語ガイドで表示されている+付き文字に対応するキーを入力した場合、2打鍵目以降も仮想鍵盤上に+付きで表示するので、ガイドに従って漢字の入力が可能です。<br>
</li><li>通常は仮想鍵盤非表示の場合でも、+付き文字に対応するキーを入力した場合、一時的に仮想鍵盤を表示するには、「熟語ガイドに従って入力する際に一時的に仮想鍵盤を表示する」の値を「仮想鍵盤」(+付き以外の文字も表示)か「熟語ガイドのみ」(+付きの文字のみ表示)に設定してください。<br>
</li><li>例:「火蓋」を入力しようとして「火」の入力後「蓋」の打ち方をど忘れした場合、Ctrl+.キーで補完。熟語ガイドで+付きの「蓋」の表示に従って1,2,3打鍵を入力。</li></ul></li></ul>

<ul><li>次の打鍵がしばらく無い場合に補完/予測入力候補を表示するには、候補ウィンドウが遅延表示に対応していれば、以下の設定で可能です。<br>
<ul><li>「候補ウィンドウの遅延表示を使用する」<br>
</li><li>「補完候補ウィンドウ表示遅延時間<code>[s]</code>」や「予測入力候補ウィンドウ表示遅延時間<code>[s]</code>」の値を1[秒]以上に設定。</li></ul></li></ul>

補完候補表示:<br>
<br>
<img src='http://uim-doc-ja.googlecode.com/svn/wiki/UimTutcodeCompletion.png' />

予測入力候補表示(交ぜ書き変換の読み入力中):<br>
<br>
<img src='http://uim-doc-ja.googlecode.com/svn/wiki/UimTutcodePrediction.png' />

仮想鍵盤上での熟語ガイド表示(0.「火」の入力後に補完):<br>
<br>
<img src='http://uim-doc-ja.googlecode.com/svn/wiki/UimTutcodeCompletionHi.png' />

仮想鍵盤上での熟語ガイド表示(1.補完で表示された熟語ガイドを見て「+蓋」が表示されているキー(QWERTYの場合はa)を打鍵):<br>
<br>
<img src='http://uim-doc-ja.googlecode.com/svn/wiki/UimTutcodeGuideFull1.png' />

仮想鍵盤上での熟語ガイド表示(2.さらに「+蓋」が表示されているキー(QWERTYの場合はv)を打鍵):<br>
<br>
<img src='http://uim-doc-ja.googlecode.com/svn/wiki/UimTutcodeGuideFull2.png' />

熟語ガイドに従って入力する際に一時的に仮想鍵盤を表示する(熟語ガイドのみ)(1'.補完で表示された熟語ガイドを見て「+蓋」が表示されているキー(QWERTYの場合はa)を打鍵):<br>
<br>
<img src='http://uim-doc-ja.googlecode.com/svn/wiki/UimTutcodeGuideOnly1.png' />

熟語ガイドに従って入力する際に一時的に仮想鍵盤を表示する(熟語ガイドのみ)(2'.さらに「+蓋」が表示されているキー(QWERTYの場合はv)を打鍵):<br>
<br>
<img src='http://uim-doc-ja.googlecode.com/svn/wiki/UimTutcodeGuideOnly2.png' />

<h2>部首合成変換時の予測入力</h2>

部首合成変換辞書を検索して、入力された部首が含まれる項目を表示。<br>
<br>
部首合成変換時の予測入力候補表示:<br>
<br>
<img src='http://uim-doc-ja.googlecode.com/svn/wiki/UimTutcodeBushuPrediction.png' />

<h2>記号入力モード</h2>

Ctrl+<code>_</code> で記号入力モードのトグル。<br>
全角英数入力モードとしても使えるようにしています。<br>
<br>
表形式の候補ウィンドウ(記号入力モード):<br>
<br>
<img src='http://uim-doc-ja.googlecode.com/svn/wiki/UimTutcodeCandwinTblKigou1.png' />

表形式の候補ウィンドウ(記号入力モードの2ページ目):<br>
<br>
<img src='http://uim-doc-ja.googlecode.com/svn/wiki/UimTutcodeCandwinTblKigou2.png' />

<h2>2ストローク記号入力モード</h2>

百相鍵盤『き』と同様に、2打鍵で各種の記号・漢字を入力するモード。<br>
漢字は基本的に文字コード順に並んでいます。<br>
(通常の記号入力モードでは、目的の文字までたどりつくために<br>
次ページキーを何回も押す必要があって面倒なので)<br>
<br>
2ストローク記号入力モード時の仮想鍵盤:<br>
<br>
<img src='http://uim-doc-ja.googlecode.com/svn/wiki/UimTutcodeKi.png' />

<h2>漢字コード入力モード</h2>

漢字コードを指定して文字を入力するモード。漢字コード入力後スペースキー<br>
(tutcode-begin-conv-key)を押すと、対応する文字が確定されます。<br>
以下の3種類の形式での入力が可能(DDSKK 14.2と同様)。<br>
<br>
<ul><li>Unicode(UCS): U+の後に16進数。U+のかわりにuでもOK(例:U+4E85またはu4e85)。(ただし、uim-tutcodeの内部コードはEUC-JP(EUC-JIS-2004)なので、JIS X 0213に無い文字(例:はしご高U+9AD9)は入力不可)<br>
</li><li>区点番号(JIS X 0213): -で区切った、面-区-点番号(面区点それぞれ10進数)。1面の場合、面-は省略可能。(例:1-48-13または48-13)<br>
</li><li>JISコード(ISO-2022-JP): 4桁の16進数。(例:502d)</li></ul>

<h2>ヒストリ入力モード</h2>

最近の部首合成変換や交ぜ書き変換、補完/予測入力、記号入力、<br>
漢字コード入力で確定した文字列を再入力するモード。<br>
「確定文字列の履歴サイズ」を1以上に設定すると有効になります。<br>
<br>
<h2>確定取り消し</h2>

直前の確定を取り消します。<br>
以下の変換では、変換後に確定される文字列を確認する機会無しに<br>
確定を行うので、意図しない漢字に確定されることがあります。<br>
この場合に、最初からの入力し直しを不要するための機能です。<br>
(確定済文字列を削除するため、uimのtext acquisition APIを使います)<br>
<br>
<ul><li>部首合成変換: 2文字目の部首入力により変換・確定開始(特に再帰的な場合)<br>
</li><li>漢字コード入力<br>
</li><li>交ぜ書き変換: 候補数が1個の時の自動確定<br>
</li><li>読み入力時のカタカナ確定、漢字→入力シーケンス確定</li></ul>

<h2>クリップボード</h2>

クリップボード内の文字列に対する以下の機能を追加しました。<br>
(クリップボードからの文字列取得のため、uimのtext acquisition APIを使用)<br>
<br>
<ul><li>クリップボード内の文字列に対してヘルプ(打ち方)を表示<br>
</li><li>クリップボード内の文字列を以下のpreeditに貼り付け<br>
<ul><li>辞書登録時<br>
</li><li>交ぜ書き変換の読み入力時<br>
</li><li>部首合成変換時("言▲▲西一早"のような部首合成シーケンスにも対応)<br>
</li><li>対話的な部首合成変換時<br>
</li><li>漢字コード入力時</li></ul></li></ul>

<h2>スクリーンショット</h2>

<img src='http://uim-doc-ja.googlecode.com/svn/wiki/UimTutcodeCandwin.png' />

候補ウィンドウ。<br>
<br>
<img src='http://uim-doc-ja.googlecode.com/svn/wiki/UimTutcodeCandwinTblMaze.png' />

表形式の候補ウィンドウ。<br>
<br>
<img src='http://uim-doc-ja.googlecode.com/svn/wiki/UimTutcodePseudoTblHelp.png' />

擬似表形式での自動へルプ表示(uim-el)。<br>
<br>
<h2>設定例</h2>

<h3>コード表の一部を変更</h3>

コード表の一部を変更したい場合は、例えば~/.uimで以下のように記述する。<br>
<pre><code>   (require "tutcode.scm")<br>
   (tutcode-rule-set-sequences!<br>
     '(((("s" " "))("―"))                ; 記号の定義を変更<br>
       ((("a" "l" "i"))("捗"))            ; 追加<br>
       ((("d" "l" "u"))("づ" "ヅ"))       ; カタカナを含む場合<br>
       ((("d" "l" "d" "u"))("っ" "ッ"))))<br>
</code></pre>

<h3>入力シーケンスにユーザ定義関数を割り当てる</h3>

selectionに対して指定した処理を適用した結果に置換する例。<br>
<br>
<pre><code>;;; 外部フィルタ<br>
;;; https://github.com/deton/uim-external-filter<br>
(require "external-filter.scm")<br>
(define (tutcode-filter-fmt-quote state pc)<br>
  (tutcode-selection-filter pc<br>
    (lambda (str)<br>
      ;; 文書整形後、引用マークを行頭に付ける (nkf -e: uim-tutcodeはEUC-JP)<br>
      (external-filter-launch-command "nkf -e -f | sed -e 's/^/&gt; /'" str))))<br>
;;; テキスト整形<br>
;;; https://github.com/deton/uim-fmt-ja<br>
(require "fmt-ja.scm")<br>
(define (tutcode-filter-fmt-ja state pc)<br>
  (tutcode-selection-filter pc<br>
    (lambda (str)<br>
      (apply string-append (fmt-ja-str str)))))<br>
;;; 半角カタカナを全角に、全角英数をASCIIに<br>
;;; https://github.com/deton/uim-japan-util<br>
(require "japan-util.scm")<br>
(define (tutcode-filter-ascii-fullkana state pc)<br>
  (tutcode-selection-filter pc<br>
    (lambda (str)<br>
      (string-list-concat<br>
        (japan-util-ascii-convert<br>
          (japan-util-halfkana-to-fullkana-convert<br>
            (string-to-list str)))))))<br>
;;; コード表に関数を登録<br>
(tutcode-rule-set-sequences!<br>
  `(((("a" "v" "q")) (,tutcode-filter-fmt-quote))<br>
    ((("a" "v" "f")) (,tutcode-filter-fmt-ja))<br>
    ((("a" "v" "a")) (,tutcode-filter-ascii-fullkana))))<br>
</code></pre>

<h2>カスタマイズ可能な項目</h2>

<h3>TUT-Codeの変数</h3>

<table><thead><th> 動作 </th><th> 変数名 </th><th> 指定できる値 </th><th> 標準値 </th></thead><tbody>
<tr><td> 交ぜ書き変換辞書ファイル </td><td> tutcode-dic-filename </td><td> "文字列"  </td><td> "/usr/local/share/tc/mazegaki.dic" </td></tr>
<tr><td> 交ぜ書き変換個人用辞書ファイル </td><td> tutcode-personal-dic-filename </td><td> "文字列"  </td><td> "$HOME/.mazegaki.dic" </td></tr>
<tr><td> コード表ファイル </td><td> tutcode-rule-filename </td><td> "文字列"  </td><td> "/usr/local/share/uim/tutcode-rule.scm" </td></tr>
<tr><td> 交ぜ書き変換の学習を有効にする </td><td> tutcode-enable-mazegaki-learning? </td><td> #t #f  </td><td> #t  </td></tr>
<tr><td> 交ぜ書き変換の学習から除外する候補数 </td><td> tutcode-mazegaki-fixed-priority-count </td><td> 数字     </td><td> 0   </td></tr>
<tr><td> 再帰学習を有効にする </td><td> tutcode-use-recursive-learning? </td><td> #t #f  </td><td> #t  </td></tr>
<tr><td> vi協調モードを有効にする </td><td> tutcode-use-with-vi? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> 入力途中のキーシーケンスを表示する </td><td> tutcode-show-pending-rk? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> Dvorakキーボードを使用する </td><td> tutcode-use-dvorak? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> 2ストローク記号入力モードを使用する </td><td> tutcode-use-kigou2-mode? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> surrounding text APIの代替方法を有効にする </td><td> tutcode-enable-fallback-surrounding-text? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> 漢字に対応しないキーシーケンスを残す </td><td> tutcode-keep-illegal-sequence? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> 後置型漢字→シーケンス変換時に直前の区切り文字を削除する </td><td> tutcode-delete-leading-delimiter-on-postfix-kanji2seq? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> 確定文字列の履歴サイズ </td><td> tutcode-history-size </td><td> 数字     </td><td> 0   </td></tr>
<tr><td> 後置型交ぜ書き変換の読みの最大文字数 </td><td> tutcode-mazegaki-yomi-max </td><td> 数字     </td><td> 10  </td></tr>
<tr><td> 交ぜ書き変換での活用する語の変換を有効にする </td><td> tutcode-mazegaki-enable-inflection? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> 交ぜ書き変換での読みの中の活用語尾の最大文字数 </td><td> tutcode-mazegaki-suffix-max </td><td> 数字     </td><td> 4   </td></tr>
<tr><td> 部首合成変換アルゴリズム </td><td> tutcode-bushu-conversion-algorithm </td><td> 'tc-2.1+ml1925<br> 'kw-yamanobe<br> 'tc-2.3.1-22.6 </td><td> 'tc-2.1+ml1925 </td></tr>
<tr><td> 対話的な部首合成変換を有効にする </td><td> tutcode-use-interactive-bushu-conversion? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> bushu.index2ファイル </td><td> tutcode-bushu-index2-filename </td><td> "文字列"  </td><td> "/usr/local/share/tc/bushu.index2" </td></tr>
<tr><td> bushu.expandファイル </td><td> tutcode-bushu-expand-filename </td><td> "文字列"  </td><td> "/usr/local/share/tc/bushu.expand" </td></tr>
<tr><td> bushu.helpファイル </td><td> tutcode-bushu-help-filename </td><td> "文字列"  </td><td> ""  </td></tr>
<tr><td> 候補ウィンドウを使用する </td><td> tutcode-use-candidate-window? </td><td> #t #f  </td><td> #t  </td></tr>
<tr><td> 擬似表形式を使用する </td><td> tutcode-use-pseudo-table-style? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> 表形式の候補ウィンドウのキー配列 </td><td> tutcode-candidate-window-table-layout </td><td> 'qwerty-jis<br> 'qwerty-us<br> 'dvorak </td><td> 'qwerty-jis </td></tr>
<tr><td> 見出し表示のキーで候補を確定する </td><td> tutcode-commit-candidate-by-label-key </td><td> 'always<br> 'havecand<br> 'candwin<br> 'never </td><td> 'always </td></tr>
<tr><td> 候補ウィンドウを表示するために変換キーを押す回数 </td><td> tutcode-candidate-op-count </td><td> 数字     </td><td> 5   </td></tr>
<tr><td> 候補ウィンドウに一度に表示する候補数 </td><td> tutcode-nr-candidate-max </td><td> 数字     </td><td> 10  </td></tr>
<tr><td> 記号モードにおいて候補ウィンドウに一度に表示する候補数 </td><td> tutcode-nr-candidate-max-for-kigou-mode </td><td> 数字     </td><td> 10  </td></tr>
<tr><td> ヒストリ入力において候補ウィンドウに一度に表示する候補数 </td><td> tutcode-nr-candidate-max-for-history </td><td> 数字     </td><td> 10  </td></tr>
<tr><td> 仮想鍵盤ウィンドウを使用する </td><td> tutcode-use-stroke-help-window? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> 何も入力していない時に仮想鍵盤ウィンドウを表示する </td><td> tutcode-show-stroke-help-window-on-no-input? </td><td> #t #f  </td><td> #t  </td></tr>
<tr><td> 自動ヘルプウィンドウを使用する </td><td> tutcode-use-auto-help-window? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> 自動ヘルプウィンドウにキーストロークを表示する </td><td> tutcode-auto-help-with-real-keys? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> 候補ウィンドウの遅延表示を使用する </td><td> tutcode-candidate-window-use-delay? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> 交ぜ書き変換候補ウィンドウ表示遅延時間<code>[s]</code> </td><td> tutcode-candidate-window-activate-delay-for-mazegaki </td><td> 数字     </td><td> 0   </td></tr>
<tr><td> 仮想鍵盤ウィンドウ表示遅延時間<code>[s]</code> </td><td> tutcode-candidate-window-activate-delay-for-stroke-help </td><td> 数字     </td><td> 2   </td></tr>
<tr><td> 自動ヘルプウィンドウ表示遅延時間<code>[s]</code> </td><td> tutcode-candidate-window-activate-delay-for-auto-help </td><td> 数字     </td><td> 1   </td></tr>
<tr><td> 補完候補ウィンドウ表示遅延時間<code>[s]</code> </td><td> tutcode-candidate-window-activate-delay-for-completion </td><td> 数字     </td><td> 2   </td></tr>
<tr><td> 予測入力候補ウィンドウ表示遅延時間<code>[s]</code> </td><td> tutcode-candidate-window-activate-delay-for-prediction </td><td> 数字     </td><td> 2   </td></tr>
<tr><td> 部首合成変換中の予測入力候補ウィンドウ表示遅延時間<code>[s]</code> </td><td> tutcode-candidate-window-activate-delay-for-bushu-prediction </td><td> 数字     </td><td> 2   </td></tr>
<tr><td> 対話的な部首合成変換候補ウィンドウ表示遅延時間<code>[s]</code> </td><td> tutcode-candidate-window-activate-delay-for-interactive-bushu </td><td> 数字     </td><td> 1   </td></tr>
<tr><td> 補完を有効にする </td><td> tutcode-use-completion? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> 補完の際に考慮する文字数の最小値 </td><td> tutcode-completion-chars-min </td><td> 数字     </td><td> 2   </td></tr>
<tr><td> 補完の際に考慮する文字数の最大値 </td><td> tutcode-completion-chars-max </td><td> 数字     </td><td> 5   </td></tr>
<tr><td> 交ぜ書き変換中の予測入力を有効にする </td><td> tutcode-use-prediction? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> 予測入力が有効になる文字数 </td><td> tutcode-prediction-start-char-count </td><td> 数字     </td><td> 2   </td></tr>
<tr><td> 熟語ガイドを有効にする </td><td> tutcode-use-kanji-combination-guide? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> 熟語ガイドに従って入力する際に一時的に仮想鍵盤を表示する </td><td> tutcode-stroke-help-with-kanji-combination-guide </td><td> 'full<br> 'guide-only<br> 'disable </td><td> 'disable </td></tr>
<tr><td> 部首合成変換中の予測入力を有効にする </td><td> tutcode-use-bushu-prediction? </td><td> #t #f  </td><td> #f  </td></tr></tbody></table>

<h4>TUT-Codeの変数の依存関係</h4>

<ul><li>tutcode-enable-mazegaki-learning? #f<br>
<ul><li>tutcode-mazegaki-fixed-priority-count</li></ul></li></ul>

<ul><li>tutcode-use-candidate-window? #f<br>
<ul><li>tutcode-candidate-op-count<br>
</li><li>tutcode-nr-candidate-max<br>
</li><li>tutcode-nr-candidate-max-for-kigou-mode<br>
</li><li>tutcode-nr-candidate-max-for-history</li></ul></li></ul>

<ul><li>tutcode-use-auto-help-window? #f<br>
<ul><li>tutcode-auto-help-with-real-keys?</li></ul></li></ul>

<ul><li>candidate-window-style 'table<br>
<ul><li>tutcode-candidate-window-table-layout</li></ul></li></ul>

<ul><li>tutcode-use-interactive-bushu-conversion? #f<br>
</li><li>tutcode-bushu-conversion-algorithm 'tc-2.3.1-22.6<br>
<ul><li>tutcode-bushu-index2-filename<br>
</li><li>tutcode-bushu-expand-filename</li></ul></li></ul>

<h3>TUT-Codeキー設定の変数</h3>

<table><thead><th> 動作 </th><th> キー変数名 </th></thead><tbody>
<tr><td> オン </td><td> tutcode-on-key? </td></tr>
<tr><td> オフ </td><td> tutcode-off-key? </td></tr>
<tr><td> ひらがな/カタカナ入力モードを反転 </td><td> tutcode-kana-toggle-key? </td></tr>
<tr><td> カタカナ入力モード </td><td> tutcode-katakana-sequence </td></tr>
<tr><td> ひらがな入力モード </td><td> tutcode-hiragana-sequence </td></tr>
<tr><td> 記号入力モードを反転 </td><td> tutcode-kigou-toggle-key? </td></tr>
<tr><td> 2ストローク記号入力モードを反転 </td><td> tutcode-kigou2-toggle-key? </td></tr>
<tr><td> 交ぜ書き変換モード </td><td> tutcode-mazegaki-start-sequence </td></tr>
<tr><td> 部首合成変換モード </td><td> tutcode-bushu-start-sequence </td></tr>
<tr><td> 対話的な部首合成変換モード </td><td> tutcode-interactive-bushu-start-sequence </td></tr>
<tr><td> 英字変換(SKK abbrev)モード </td><td> tutcode-latin-conv-start-sequence </td></tr>
<tr><td> 漢字コード入力モード </td><td> tutcode-kanji-code-input-start-sequence </td></tr>
<tr><td> ヒストリ入力モード </td><td> tutcode-history-start-sequence </td></tr>
<tr><td> 直近の自動ヘルプを表示 </td><td> tutcode-auto-help-redisplay-sequence </td></tr>
<tr><td> 直近の自動ヘルプ内容を確定 </td><td> tutcode-auto-help-dump-sequence </td></tr>
<tr><td> 交ぜ書き変換の読みをカタカナとして確定する </td><td> tutcode-katakana-commit-key? </td></tr>
<tr><td> 仮想鍵盤ウィンドウの表示を反転 </td><td> tutcode-stroke-help-toggle-key? </td></tr>
<tr><td> 補完開始 </td><td> tutcode-begin-completion-key? </td></tr>
<tr><td> 変換開始 </td><td> tutcode-begin-conv-key? </td></tr>
<tr><td> 確定 </td><td> tutcode-commit-key? </td></tr>
<tr><td> キャンセル </td><td> tutcode-cancel-key? </td></tr>
<tr><td> 次候補 </td><td> tutcode-next-candidate-key? </td></tr>
<tr><td> 前候補 </td><td> tutcode-prev-candidate-key? </td></tr>
<tr><td> 確定取り消し </td><td> tutcode-undo-sequence </td></tr>
<tr><td> 現在位置の文字のヘルプを表示 </td><td> tutcode-help-sequence </td></tr>
<tr><td> クリップボード内文字列のヘルプを表示 </td><td> tutcode-help-clipboard-sequence </td></tr>
<tr><td> クリップボードから貼り付け </td><td> tutcode-paste-key? </td></tr>
<tr><td> クリップボード内文字列をシーケンス→漢字変換 </td><td> tutcode-clipboard-seq2kanji-start-sequence </td></tr>
<tr><td> セレクションを交ぜ書き変換 </td><td> tutcode-selection-mazegaki-start-sequence </td></tr>
<tr><td> セレクションを交ぜ書き変換 (活用する語) </td><td> tutcode-selection-mazegaki-inflection-start-sequence </td></tr>
<tr><td> セレクションをカタカナ変換 </td><td> tutcode-selection-katakana-start-sequence </td></tr>
<tr><td> セレクションを漢字→シーケンス変換 </td><td> tutcode-selection-kanji2seq-start-sequence </td></tr>
<tr><td> セレクションをシーケンス→漢字変換 </td><td> tutcode-selection-seq2kanji-start-sequence </td></tr>
<tr><td> 候補ウィンドウの次ページ </td><td> tutcode-next-page-key? </td></tr>
<tr><td> 候補ウィンドウの前ページ </td><td> tutcode-prev-page-key? </td></tr>
<tr><td> バックスペース </td><td> tutcode-backspace-key? </td></tr>
<tr><td> リターン </td><td> tutcode-return-key? </td></tr>
<tr><td> vi協調モードでESCとして扱うキー </td><td> tutcode-vi-escape-key? </td></tr>
<tr><td> 交ぜ書き変換個人辞書への単語登録 </td><td> tutcode-register-candidate-key? </td></tr>
<tr><td> 交ぜ書き変換個人辞書からの単語削除 </td><td> tutcode-purge-candidate-key? </td></tr>
<tr><td> 交ぜ書き変換で読みを伸ばす </td><td> tutcode-mazegaki-relimit-left-key? </td></tr>
<tr><td> 交ぜ書き変換で読みを縮める </td><td> tutcode-mazegaki-relimit-right-key? </td></tr>
<tr><td> 入力途中のキーストロークを挿入 </td><td> tutcode-verbose-stroke-key? </td></tr>
<tr><td> 後置型部首合成変換 </td><td> tutcode-postfix-bushu-start-sequence </td></tr>
<tr><td> 後置型交ぜ書き変換開始 (活用しない語) </td><td> tutcode-postfix-mazegaki-start-sequence </td></tr>
<tr><td> 後置型交ぜ書き変換開始 (読み1文字) </td><td> tutcode-postfix-mazegaki-1-start-sequence </td></tr>
<tr><td> 後置型交ぜ書き変換開始 (読み2文字) </td><td> tutcode-postfix-mazegaki-2-start-sequence </td></tr>
<tr><td> 後置型交ぜ書き変換開始 (読み3文字) </td><td> tutcode-postfix-mazegaki-3-start-sequence </td></tr>
<tr><td> 後置型交ぜ書き変換開始 (読み4文字) </td><td> tutcode-postfix-mazegaki-4-start-sequence </td></tr>
<tr><td> 後置型交ぜ書き変換開始 (読み5文字) </td><td> tutcode-postfix-mazegaki-5-start-sequence </td></tr>
<tr><td> 後置型交ぜ書き変換開始 (読み6文字) </td><td> tutcode-postfix-mazegaki-6-start-sequence </td></tr>
<tr><td> 後置型交ぜ書き変換開始 (読み7文字) </td><td> tutcode-postfix-mazegaki-7-start-sequence </td></tr>
<tr><td> 後置型交ぜ書き変換開始 (読み8文字) </td><td> tutcode-postfix-mazegaki-8-start-sequence </td></tr>
<tr><td> 後置型交ぜ書き変換開始 (読み9文字) </td><td> tutcode-postfix-mazegaki-9-start-sequence </td></tr>
<tr><td> 後置型交ぜ書き変換開始 (活用する語) </td><td> tutcode-postfix-mazegaki-inflection-start-sequence </td></tr>
<tr><td> 後置型交ぜ書き変換開始 (活用する語,読み1文字) </td><td> tutcode-postfix-mazegaki-inflection-1-start-sequence </td></tr>
<tr><td> 後置型交ぜ書き変換開始 (活用する語,読み2文字) </td><td> tutcode-postfix-mazegaki-inflection-2-start-sequence </td></tr>
<tr><td> 後置型交ぜ書き変換開始 (活用する語,読み3文字) </td><td> tutcode-postfix-mazegaki-inflection-3-start-sequence </td></tr>
<tr><td> 後置型交ぜ書き変換開始 (活用する語,読み4文字) </td><td> tutcode-postfix-mazegaki-inflection-4-start-sequence </td></tr>
<tr><td> 後置型交ぜ書き変換開始 (活用する語,読み5文字) </td><td> tutcode-postfix-mazegaki-inflection-5-start-sequence </td></tr>
<tr><td> 後置型交ぜ書き変換開始 (活用する語,読み6文字) </td><td> tutcode-postfix-mazegaki-inflection-6-start-sequence </td></tr>
<tr><td> 後置型交ぜ書き変換開始 (活用する語,読み7文字) </td><td> tutcode-postfix-mazegaki-inflection-7-start-sequence </td></tr>
<tr><td> 後置型交ぜ書き変換開始 (活用する語,読み8文字) </td><td> tutcode-postfix-mazegaki-inflection-8-start-sequence </td></tr>
<tr><td> 後置型交ぜ書き変換開始 (活用する語,読み9文字) </td><td> tutcode-postfix-mazegaki-inflection-9-start-sequence </td></tr>
<tr><td> 後置型カタカナ変換開始 </td><td> tutcode-postfix-katakana-start-sequence </td></tr>
<tr><td> 後置型カタカナ変換 (ひらがなが続く間) </td><td> tutcode-postfix-katakana-0-start-sequence </td></tr>
<tr><td> 後置型カタカナ変換 (1文字) </td><td> tutcode-postfix-katakana-1-start-sequence </td></tr>
<tr><td> 後置型カタカナ変換 (2文字) </td><td> tutcode-postfix-katakana-2-start-sequence </td></tr>
<tr><td> 後置型カタカナ変換 (3文字) </td><td> tutcode-postfix-katakana-3-start-sequence </td></tr>
<tr><td> 後置型カタカナ変換 (4文字) </td><td> tutcode-postfix-katakana-4-start-sequence </td></tr>
<tr><td> 後置型カタカナ変換 (5文字) </td><td> tutcode-postfix-katakana-5-start-sequence </td></tr>
<tr><td> 後置型カタカナ変換 (6文字) </td><td> tutcode-postfix-katakana-6-start-sequence </td></tr>
<tr><td> 後置型カタカナ変換 (7文字) </td><td> tutcode-postfix-katakana-7-start-sequence </td></tr>
<tr><td> 後置型カタカナ変換 (8文字) </td><td> tutcode-postfix-katakana-8-start-sequence </td></tr>
<tr><td> 後置型カタカナ変換 (9文字) </td><td> tutcode-postfix-katakana-9-start-sequence </td></tr>
<tr><td> 後置型カタカナ変換 (1文字除く) </td><td> tutcode-postfix-katakana-exclude-1-sequence </td></tr>
<tr><td> 後置型カタカナ変換 (2文字除く) </td><td> tutcode-postfix-katakana-exclude-2-sequence </td></tr>
<tr><td> 後置型カタカナ変換 (3文字除く) </td><td> tutcode-postfix-katakana-exclude-3-sequence </td></tr>
<tr><td> 後置型カタカナ変換 (4文字除く) </td><td> tutcode-postfix-katakana-exclude-4-sequence </td></tr>
<tr><td> 後置型カタカナ変換 (5文字除く) </td><td> tutcode-postfix-katakana-exclude-5-sequence </td></tr>
<tr><td> 後置型カタカナ変換 (6文字除く) </td><td> tutcode-postfix-katakana-exclude-6-sequence </td></tr>
<tr><td> 後置型カタカナ変換 (1文字縮め) </td><td> tutcode-postfix-katakana-shrink-1-sequence </td></tr>
<tr><td> 後置型カタカナ変換 (2文字縮め) </td><td> tutcode-postfix-katakana-shrink-2-sequence </td></tr>
<tr><td> 後置型カタカナ変換 (3文字縮め) </td><td> tutcode-postfix-katakana-shrink-3-sequence </td></tr>
<tr><td> 後置型カタカナ変換 (4文字縮め) </td><td> tutcode-postfix-katakana-shrink-4-sequence </td></tr>
<tr><td> 後置型カタカナ変換 (5文字縮め) </td><td> tutcode-postfix-katakana-shrink-5-sequence </td></tr>
<tr><td> 後置型カタカナ変換 (6文字縮め) </td><td> tutcode-postfix-katakana-shrink-6-sequence </td></tr>
<tr><td> 後置型漢字→シーケンス変換開始 </td><td> tutcode-postfix-kanji2seq-start-sequence </td></tr>
<tr><td> 後置型漢字→シーケンス変換 (1文字) </td><td> tutcode-postfix-kanji2seq-1-start-sequence </td></tr>
<tr><td> 後置型漢字→シーケンス変換 (2文字) </td><td> tutcode-postfix-kanji2seq-2-start-sequence </td></tr>
<tr><td> 後置型漢字→シーケンス変換 (3文字) </td><td> tutcode-postfix-kanji2seq-3-start-sequence </td></tr>
<tr><td> 後置型漢字→シーケンス変換 (4文字) </td><td> tutcode-postfix-kanji2seq-4-start-sequence </td></tr>
<tr><td> 後置型漢字→シーケンス変換 (5文字) </td><td> tutcode-postfix-kanji2seq-5-start-sequence </td></tr>
<tr><td> 後置型漢字→シーケンス変換 (6文字) </td><td> tutcode-postfix-kanji2seq-6-start-sequence </td></tr>
<tr><td> 後置型漢字→シーケンス変換 (7文字) </td><td> tutcode-postfix-kanji2seq-7-start-sequence </td></tr>
<tr><td> 後置型漢字→シーケンス変換 (8文字) </td><td> tutcode-postfix-kanji2seq-8-start-sequence </td></tr>
<tr><td> 後置型漢字→シーケンス変換 (9文字) </td><td> tutcode-postfix-kanji2seq-9-start-sequence </td></tr>
<tr><td> 後置型シーケンス→漢字変換開始 </td><td> tutcode-postfix-seq2kanji-start-sequence </td></tr>
<tr><td> 後置型シーケンス→漢字変換 (1文字) </td><td> tutcode-postfix-seq2kanji-1-start-sequence </td></tr>
<tr><td> 後置型シーケンス→漢字変換 (2文字) </td><td> tutcode-postfix-seq2kanji-2-start-sequence </td></tr>
<tr><td> 後置型シーケンス→漢字変換 (3文字) </td><td> tutcode-postfix-seq2kanji-3-start-sequence </td></tr>
<tr><td> 後置型シーケンス→漢字変換 (4文字) </td><td> tutcode-postfix-seq2kanji-4-start-sequence </td></tr>
<tr><td> 後置型シーケンス→漢字変換 (5文字) </td><td> tutcode-postfix-seq2kanji-5-start-sequence </td></tr>
<tr><td> 後置型シーケンス→漢字変換 (6文字) </td><td> tutcode-postfix-seq2kanji-6-start-sequence </td></tr>
<tr><td> 後置型シーケンス→漢字変換 (7文字) </td><td> tutcode-postfix-seq2kanji-7-start-sequence </td></tr>
<tr><td> 後置型シーケンス→漢字変換 (8文字) </td><td> tutcode-postfix-seq2kanji-8-start-sequence </td></tr>
<tr><td> 後置型シーケンス→漢字変換 (9文字) </td><td> tutcode-postfix-seq2kanji-9-start-sequence </td></tr></tbody></table>

<h3>tutcode-ruleの変数</h3>

<table><thead><th> 動作 </th><th> 変数名 </th><th> 指定できる値 </th><th> 標準値 </th></thead><tbody>
<tr><td> 新常用漢字に対応したTUT+コードを使用する </td><td> tutcode-rule-use-tutplus? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> 大文字でひらがな/カタカナ反転入力する </td><td> tutcode-rule-uppercase-as-opposite-kana? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> 大文字でカタカナ入力するルールを含めない </td><td> tutcode-rule-exclude-uppercase-for-katakana? </td><td> #t #f  </td><td> #f  </td></tr>
<tr><td> 大文字でカタカナ入力するルールに記号を含めない </td><td> tutcode-rule-exclude-uppercase-for-kigou-in-katakana? </td><td> #t #f  </td><td> #f  </td></tr></tbody></table>

<h2>ファイル</h2>

<ul><li>UimPrefが更新するファイル<br>
<ul><li>~/.uim.d/customs/custom-tutcode.scm:: <a href='UimPref.md'>UimPref</a>の「TUT-Code」ファイル。<br>
</li><li>~/.uim.d/customs/custom-tutcode-keys{1,2}.scm:: <a href='UimPref.md'>UimPref</a>の「TUT-Code キー設定{1,2}」ファイル。<br>
</li></ul></li><li>UimTutcodeが更新するファイル<br>
<ul><li>~/.mazegaki.dic:: 交ぜ書き変換個人用辞書ファイル。