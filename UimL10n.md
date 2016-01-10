= 翻訳 =

[uim:po/ja.po](http://uim.googlecode.com/svn/trunk/po/ja.po)より転載

## 諸規則 ##

  * 意訳優先。原意が多少損われても気にしない
  * 簡潔に。わかりやすくするつもりで冗長な文にしない
  * 体言止めを基本とする。文末に「〜です」等を付加しない
  * boolean設定の説明は「〜を有効にする」「〜を使用する」のように「する」で終える
  * カタカナ語の語尾は延ばさない(「サーバー」ではなく「サーバ」とする)
    * JIS Z8301:2005 表 G.3 - 外来語の表記に語尾の長音符号を除く場合の原則
  * 英数記号はASCII(半角)で表記し、全角文字は使わない
  * 日本語の複合語中に英字表記の語が含まれても語境界にスペースを入れない。"uim アプレット" や "ATOK 風" ではなく "uimアプレット" "ATOK風" とする
    * 日本語文中に英単語が現れた場合スペースを入れる作法が普及しているが、本ファイル中では日本語に訳さないと意味を為さないので基本的にそのような状況は発生しないはず(uim, GNOME等の固有名詞は日本語の単語と同様に扱う)。もし必要になったらその時議論する
    * http://www.otsune.com/diary/2006/06/21/1.html
  * 漢字圏の外国語に由来する用語は日本語で一般に使われている表現を用いる。その言語でネイティブに使われている用語も漢語ゆえ日本語話者にも理解可能であるが(例: 「中文」)、あくまで外国語であり一般の日本語話者には不自然であったり理解不能な場合がある事を念頭に置く
  * 言語名と国名は区別する。基本的にja.wikipedia.orgに見出しのある言語名を採用する
    * [wikipedia:ISO\_639](http://ja.wikipedia.org/wiki/ISO_639)
    * Wikipedia側が不適切と思われる場合はそちらも修正する
    * 日本語においては「ベンガル語」で統一されているようなので(Bangla)は訳さない
  * "Anthy"と"Anthy キー設定1"のように関連するグループ名は同じ"Anthy"で始める事によって関連を示す。その際従属するグループ名では"Anthy キー設定1"のようにスペースを空けて"Anthy"が名前空間を形成している事を視覚的に示す

## 日本語訳に使用する用語 (適宜追加お願いします) ##

  * advanced:: 高度(な)
  * annotation:: 註釈
  * beol:: ボル
  * beol-sik:: ボル式
  * binding(s):: 設定 (状況に応じて他の訳も可)
  * cancel:: キャンセル (「取消」はeraseの意を含むので避ける)
  * candidate:: 候補
  * Chinese:: 中国語 (「中文」は一般に知られていない外国語なので避ける)
  * commit:: 確定
  * compose, composition:: 構成 (文脈により「合成」)
  * cursor, caret:: カーソル
  * default:: 標準
  * deploy:: 状況に応じて適切に意訳。「配備」はものものしいので使わない
  * Emacs:: Emacs (固有名詞として)
  * emacs:: emacs (コマンドとして)
  * enable:: 有効 (状況に応じて他の訳も可。availableとの誤認を避けるよう留意)
  * Enter:: Enter
  * ESC, escape:: ESC
  * fullwidth alphanumeric:: 全角英数(字) (label中では「字」を入れず、short-descには入れる)
  * global:: 全体 (状況に応じて他の訳も可。「全般」はgenericの意を含むので避ける)
  * hot key:: ホットキー (shortcutとショートカットの方がいいかもしれない。要議論)
  * International Phonetic Alphabet (IPA):: 国際音声記号
  * input method:: 入力方式 (ただし、デスクトップ環境を構築する機構としてのinput methodを指す場合等は「入力メソッド」も用いる)
  * item:: 項目 (状況に応じて他の訳も可)
  * key bindings:: キー設定
  * mode:: モード
  * '''modifier key''':: 修飾キー
  * off:: オフ
  * on:: オン
  * pinyin:: ピンイン (「拼音」等は認知度が低いので外来語としてカタカナ表記)
  * preference:: 設定
  * preedit:: 編集領域
  * quit:: 終了
  * Return, return:: リターン
  * save:: 保存
  * separator:: 区切り
  * simplified Chinese:: 簡体字(中国語)
  * status:: 状態switch:: 切り換え(る)
  * traditional Chinese:: 繁体字(中国語)
  * transition:: 遷移 (ただし、わかりにくいという意見が多ければ「移行」等に)
  * transposed:: (置き換えて、反転して)
  * toggle:: 反転 (状況に応じて他の訳も可。「トグル」は携帯電話の入力方式等で誤用が広まっているので避ける)
  * Uim, UIM:: uim
  * Unicode:: ユニコード
  * Unix, unix:: UNIX
  * use:: 使用
  * Vi, vi:: vi (固有名詞、コマンド共)