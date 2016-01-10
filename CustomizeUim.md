= カスタマイズ =



## カスタマイズ方法 ##

カスタマイズは[UimPref](UimPref.md)というGUI設定ツール、もしくは~/.uimファイルに自分で記述して行います。 ~/.uimファイルがない場合は$prefix/share/uim/default.scmが読まれます。

[UimPref](UimPref.md)による設定は~/.uim.d/customs以下のファイルに書き込まれますが、'''~/.uimに記述した設定はそれを上書きします。''' [UimPref](UimPref.md)の設定を使う場合、~/.uimから[UimPref](UimPref.md)の設定と矛盾する記述を取り除いてください。

### カスタマイズの適用先を限定 ###

LIBUIM\_USER\_SCM\_FILE環境変数を利用することで、一時的にカスタマイズを適用したり、異なるアプリに別々のカスタマイズを適用することができます。

```
Firefoxでuim-anthyの候補ウィンドウを出さない例:
$ echo '(define anthy-use-candidate-window? #f)' > ~/.uim-firefox
$ LIBUIM_USER_SCM_FILE=~/.uim-firefox firefox &
```

## カスタマイズの注意点 ##

### ~/.uimから変更できない特別な設定 ###

  * enable-lazy-loading?
  * enabled-im-list
  * installed-im-module-list

上記の変数に関する設定は、~/.uimに記述しても変更する事ができません。 変更するには[UimPref](UimPref.md)で設定するか、$prefix/share/uim/installed-modules.scmを直接編集してください。

### 文字コード ###

ファイル中の日本語はすべて'''EUC-JP'''で記述してください。 例えばvimを使っているなら、ファイルの末尾あたりに

```
;; vim:ft=scheme:fenc=euc-jp
```

Emacsであれば

```
;; Local Variables:
;; mode: scheme
;; coding: euc-jp
;; End:
```

などと書いておくと便利かもしれません。

### 記述ミス ###

記述に致命的な不備があっても、エラーメッセージなどを出さず、ただ無視されます。それらは

```
$ uim-sh ~/.uim
```

を実行すれば発見できるかもしれません。

## 入力方式のカスタマイズ ##

### 一般 ###

基本的な書式

```
(require-module "モジュール名")
(define 変数名 値)
(define 変数名 値)
...
```

指定可能なモジュール名を取得するには、[UimSh](UimSh.md)で以下を実行してください。

```
uim> installed-im-module-list
```

有効無効を指定する変数では、'''#t'''は有効、'''#f'''は無効を表します。

```
(define generic-use-candidate-window? #t)
```

任意の文字を指定できる変数では文字を'''""'''で囲む必要があります。

```
(define canna-segment-separator "|")
```

数字を指定する変数ではそのまま。

```
(define generic-candidate-op-count 1)
```

決められた文字列を指定する変数では文字列の先頭に'''''''がつきます。

```
(define default-im-name 'anthy)
```

### ホットキー ###

基本的な書式

```
(require-module "モジュール名")
(define-key キー変数名 '("キー名"))
(define-key キー変数名 '("キー名"))
...
```

キー名を複数指定する場合はスペースで区切ります。

```
(define-key generic-on-key? '("a" "b"))
```

また別のキー変数名を指定する事でキー指定を同期させる事ができます。

```
(define-key generic-on-key? '("a" "b"))
(define-key anthy-on-key? '(generic-on-key? "c"))
```

修飾キーは<>で囲みます。

```
(define-key generic-on-key? '("<Shift>a"))
```

また修飾キーを一般のキーとして使う時は\_keyをつけます

```
(define-key generic-on-key? '("<Control>Alt_key"))
```

キー名の表記方法は[UimFep](UimFep.md)の'''-K'''オプションが役に立ちます。

### キー名（抜粋） ###

#### 一般キー ####

| uim | Xmodmap |
|:----|:--------|
| " " | "space" |
| "up" | "Up"    |
| "down" | "Down"  |
| "left" | "Left"  |
| "right" | "Right" |
| "home" | "Home"  |
| "next" | "Next"  |
| "prior" | "Prior" |
| "delete" | "Delete" |
| "end" | "End"   |
| "insert" | "Insert" |
| "backspace" | "BackSpace" |
| "return" | "Return" |
| "tab" | "Tab"   |
| "F1" | "F1"    |
| "F35" | "F35"   |

#### 修飾キー ####

| uim | Xmodmap |
|:----|:--------|
| "

&lt;Control&gt;

" | "Control\_L" "Control\_R" |
| "

&lt;Alt&gt;

" | "Alt\_L" "Alt\_R" |
| "

&lt;Shift&gt;

" | "Shift\_L" "Shift\_R" |
| "

&lt;Meta&gt;

" | "Meta\_L" "Meta\_R" |
| "

&lt;Super&gt;

" | "Super\_L" "Super\_R" |
| "

&lt;Hyper&gt;

" | "Hyper\_L" "Hyper\_R" |

#### スペシャルキー ####

| uim | Xmodmap |
|:----|:--------|
| "Multi\_key" | "Multi\_key" |
| "codeinput" | "Codeinput" |
| "single-candidate" | "SingleCandidate" |
| "multiple-candidate" | "MultipleCandidate" |
| "previous-candidate" | "PreviousCandidate" |
| "Mode\_switch" | "Mode\_switch" |
| "Kanji" | "Kanji" |
| "Muhenkan" | "Muhenkan" |
| "Henkan\_Mode" | "Henkan\_Mode" |
| "romaji" | "Romaji" |
| "hiragana" | "Hiragana" |
| "katakana" | "Katakana" |
| "hiragana-katakana" | "Hiragana\_Katakana" |
| "zenkaku" | "Zenkaku" |
| "hankaku" | "Hankaku" |
| "zenkaku-hankaku" | "Zenkaku\_Hankaku" |
| "touroku" | "Touroku" |
| "massyo" | "Massyo" |
| "kana-lock" | "Kana\_Lock" |
| "kana-shift" | "Kana\_Shift" |
| "eisu-shift" | "Eisu\_Shift" |
| "eisu-toggle | "Eisu\_toggle" |
| "Private1" |
| "Private30" |

### UimAnthy uim-anthy ###

基本的な書式

```
(require-module "anthy")
(define 変数名 値)
(define 変数名 値)
...
```

#### Shift+アルファベットキーで大文字アルファベットを直接入力 ####

[ftp://ftp.linet.gr.jp/pub/Plamo/Plamo-4.2/contrib/FEP/](ftp://ftp.linet.gr.jp/pub/Plamo/Plamo-4.2/contrib/FEP/)

#### 確定前入力文字がある状態でスペースを入力 ####

http://pc10.2ch.net/test/read.cgi/linux/1135968795/581

```
--- /usr/local/share/uim/anthy.scm.orig
+++ /usr/local/share/uim/anthy.scm
@@ -1092,9 +1092,9 @@
　　　　(ustr-cursor-move-end! raw-str))

　　　　;; modifiers (except shift) => ignore
-　　　 ((and (modifier-key-mask key-state)
-　　　　　　(not (shift-key-mask key-state)))
-　　　 #f)
+;;　　　 ((and (modifier-key-mask key-state)
+;;　　　　　(not (shift-key-mask key-state)))
+;;　　 #f)

　　　　((symbol? key)
　　　　 #f)
```

~/.uimに

```
(require "japanese.scm")
(define ja-rk-rule-basic (append '((((" ") . ())(" " " " " "))) ja-rk-rule-basic))
(ja-rk-rule-update)
```

で、修飾キー+SPC。

### UimSkk uim-skk ###

基本的な書式

```
(require-module "skk")
(define 変数名 値)
(define 変数名 値)
...
```

#### 編集領域のビジュアルスタイルを独自のスタイルに ####

基本的な書式

```
(require-module "skk")
(define skk-style-スタイル名
  '((変数名 . 値)
...
    (変数名 . 値)))
(define skk-style 'skk-style-スタイル名)
```

```
; 例
(require-module "skk")
(define skk-style-simple
  '((skk-preedit-attr-mode-mark            . preedit-none)
    (skk-preedit-attr-head                 . preedit-none)
    (skk-preedit-attr-okuri                . preedit-none)
    (skk-preedit-attr-pending-rk           . preedit-none)
    (skk-preedit-attr-conv-body            . preedit-none)
    (skk-preedit-attr-conv-okuri           . preedit-none)
    (skk-preedit-attr-conv-appendix        . preedit-none)
    (skk-preedit-attr-direct-pending-rk    . preedit-none)
    (skk-preedit-attr-child-beginning-mark . preedit-none)
    (skk-preedit-attr-child-end-mark       . preedit-none)
    (skk-preedit-attr-child-committed      . preedit-none)
    (skk-preedit-attr-child-dialog         . preedit-none)
    (skk-preedit-attr-dcomp                . preedit-none)
    (skk-child-context-beginning-mark      . "[")
    (skk-child-context-end-mark            . "]")
    (skk-show-cursor-on-preedit?           . #t)
    (skk-show-candidates-with-okuri?       . #f)))
(define skk-style 'skk-style-simple)
```

| 動作 | 変数名 | 指定できる値 |
|:---|:----|:-------|
| モードマーク | skk-preedit-attr-mode-mark | preedit-none<br> preedit-reverse<br> preedit-underline<br> preedit-cursor<br> preedit-separator <br>
<tr><td> ▽モードの見出し語 </td><td> skk-preedit-attr-head </td><td> preedit-none<br> preedit-reverse<br> preedit-underline<br> preedit-cursor<br> preedit-separator </td></tr>
<tr><td> 再帰学習モードの送り仮名 </td><td> skk-preedit-attr-okuri </td><td> preedit-none<br> preedit-reverse<br> preedit-underline<br> preedit-cursor<br> preedit-separator </td></tr>
<tr><td> ▽モードのローマ字プレフィックス </td><td> skk-preedit-attr-pending-rk </td><td> preedit-none<br> preedit-reverse<br> preedit-underline<br> preedit-cursor<br> preedit-separator </td></tr>
<tr><td> ▼モードの見出し語 </td><td> skk-preedit-attr-conv-body </td><td> preedit-none<br> preedit-reverse<br> preedit-underline<br> preedit-cursor<br> preedit-separator </td></tr>
<tr><td> ▼モードの送り仮名 </td><td> skk-preedit-attr-conv-okuri </td><td> preedit-none<br> preedit-reverse<br> preedit-underline<br> preedit-cursor<br> preedit-separator </td></tr>
<tr><td>    </td><td> skk-preedit-attr-conv-appendix </td><td> preedit-none<br> preedit-reverse<br> preedit-underline<br> preedit-cursor<br> preedit-separator </td></tr>
<tr><td> ローマ字プレフィックス </td><td> skk-preedit-attr-direct-pending-rk </td><td> preedit-none<br> preedit-reverse<br> preedit-underline<br> preedit-cursor<br> preedit-separator </td></tr>
<tr><td> 再帰学習エリアの先頭 </td><td> skk-preedit-attr-child-beginning-mark </td><td> preedit-none<br> preedit-reverse<br> preedit-underline<br> preedit-cursor<br> preedit-separator </td></tr>
<tr><td> 再帰学習エリアの終わり </td><td> skk-preedit-attr-child-end-mark </td><td> preedit-none<br> preedit-reverse<br> preedit-underline<br> preedit-cursor<br> preedit-separator </td></tr>
<tr><td> 再帰学習エリア </td><td> skk-preedit-attr-child-committed </td><td> preedit-none<br> preedit-reverse<br> preedit-underline<br> preedit-cursor<br> preedit-separator </td></tr>
<tr><td> 単語削除エリア </td><td> skk-preedit-attr-child-dialog </td><td> preedit-none<br> preedit-reverse<br> preedit-underline<br> preedit-cursor<br> preedit-separator </td></tr>
<tr><td> 動的補完エリア </td><td> skk-preedit-attr-dcomp </td><td> preedit-none<br> preedit-reverse<br> preedit-underline<br> preedit-cursor<br> preedit-separator </td></tr>
<tr><td> 再帰学習エリアの先頭を示す文字 </td><td> skk-child-context-beginning-mark </td><td> "文字"   </td></tr>
<tr><td> 再帰学習エリアの終わりを示す文字 </td><td> skk-child-context-end-mark </td><td> "文字"   </td></tr>
<tr><td> ▽モードで文字を入力している時にカーソルを表示するか </td><td> skk-show-cursor-on-preedit? </td><td> #t #f  </td></tr>
<tr><td> 候補選択ウィンドウ中に表示される候補に送り仮名を付加するか </td><td> skk-show-candidates-with-okuri? </td><td> #t #f  </td></tr></tbody></table>

<h4>変換候補の見出しキーを変更する</h4>

<pre><code>(require-module "skk")<br>
(define skk-ddskk-like-heading-label-char-list '("a" "s" "d" "f" "j" "k" "l"))<br>
</code></pre>

<h4>自動変換を始める文字を変更する</h4>

<pre><code>(require-module "skk")<br>
(define skk-auto-start-henkan-keyword-list<br>
  '("を" "、" "。" "．" "，" "？" "」" "！" "；" "：" ")" ";" ":" "）" "”"<br>
    "】" "』" "》" "〉" "｝" "］" "〕" "}" "]" "?" "." "," "!"))<br>
</code></pre>

<h4>キャンセルした後に動的補完を表示しない</h4>

$prefix/share/uim/skk.scmに2箇所ある<br>
<br>
<pre><code>;; don't clear dcomp (not compatible with ddskk's behavior)<br>
;;(skk-reset-dcomp-word sc)<br>
</code></pre>

のコメントを外してください。<br>
<br>
<h3>UimPrime uim-prim</h3>

基本的な書式<br>
<br>
<pre><code>(require-module "prime")<br>
(define キー変数名 '("キー名")<br>
(define キー変数名 '("キー名")<br>
...<br>
</code></pre>

<table><thead><th> 動作 </th><th> キー変数名 </th></thead><tbody>
<tr><td> 全角スペース </td><td> prime-space-key? </td></tr>
<tr><td> 半角スペース </td><td> prime-altspace-key? </td></tr></tbody></table>

<h3>UimFep uim-fep</h3>

<h4>全角/半角キーでオン/オフ</h4>

全角/半角キーは端末では認識できないので、端末で認識できるキーシーケンスを割り当てます。 ここでは全角/半角キーをF10にしますが、この場合、端末以外のアプリケーションでも全角/半角キーがF10になるので注意してください。<br>
<br>
ktermを使っている場合、~/.Xresource（~/.Xdefaults）に次のように書きます。<br>
<br>
<pre><code>kterm.VT100.Translations: #override \<br>
  &lt;Key&gt;Zenkaku_Hankaku: string("\033[21~")<br>
</code></pre>

xtermを使っている場合、~/.Xresource（~/.Xdefaults）に次のように書きます。<br>
<br>
<pre><code>xterm.VT100.Translations: #override \<br>
  &lt;Key&gt;Zenkaku_Hankaku: string("\033[21~")<br>
</code></pre>

rxvtを使っている場合、~/.Xresource（~/.Xdefaults）に次のように書きます。<br>
<br>
<pre><code>rxvt.keysym.Zenkaku_Hankaku: "\033[21~"<br>
</code></pre>

atermを使っている場合、~/.Xresource（~/.Xdefaults）に次のように書きます。<br>
<br>
<pre><code>aterm.keysym.Zenkaku_Hankaku: "\033[21~"<br>
</code></pre>

そしてログインしなおすか、次のコマンドを入力します。<br>
<br>
<pre><code>$ xrdb -m ~/.Xresources<br>
</code></pre>

mltermを使っている場合、~/.mlterm/keyに次のように書きます。<br>
<br>
<pre><code>Zenkaku_Hankaku="^[21~"<br>
</code></pre>

^[21~の部分はF10のキーシーケンスです。 vimではCtrl+v F10、emacsではCtrl+q F10で入力できます。<br>
<br>
Etermを使っている場合、~/.Eterm/user.cfgに次のように書きます。<br>
<br>
<pre><code>&lt;Eterm-0.9&gt;<br>
begin actions<br>
  bind Zenkaku_Hankaku to echo "\e[21~"<br>
end actions<br>
</code></pre>

その他のXの端末を使っている場合 ~/.Xmodmapに次のように書きます。<br>
<br>
<pre><code>keysym Zenkaku_Hankaku = F10<br>
</code></pre>

ログインしなおすか、次のコマンドを入力します。<br>
<br>
<pre><code>$ xmodmap ~/.Xmodmap<br>
</code></pre>

teratermを使っている場合、TTERMPRO\keycode.exeを起動して全角/半角キーのキーコードを調べます。 全角/半角キーのキーコードは41であることが分かります。 TTERMPRO\KEYBOARDに次のように書きます。<br>
<br>
<pre><code>[User Keys]<br>
User1=41,0,$1b[21~<br>
</code></pre>

しかし全角/半角キーを押してもWindowsのIMEに取られるので使えません。<br>
<br>
Linuxコンソールではloadkeysを使ってキーシーケンスを変えることができます。 まずキーマップの定義ファイルを編集します。 キーマップの定義ファイルはLinuxディストリビューションによってはパスが違うかもしれません。<br>
<br>
<pre><code>$ zcat /lib/kbd/keymaps/i386/qwerty/jp106.map.gz &gt; jp.map<br>
$ echo 'keycode  41 = F10' &gt;&gt; jp.map<br>
</code></pre>

keycodeの41は全角/半角キーに対応しています。 showkeyコマンドで確かめてください。 showkeyは10秒間入力しないと終了します。<br>
<br>
loadkeysでこのキーマップを読み込めば全角/半角キーがF10になります。<br>
<br>
<pre><code>$ loadkeys jp<br>
</code></pre>

Debianではキーマップの定義ファイルを編集する必要はありません。<br>
<br>
<pre><code># echo 's/keycode  41 = Escape/Keycode  41 = F10/;' &gt;&gt; /etc/console-tools/remap<br>
# /etc/init.d/console-screen.sh（その場で有効化）<br>
</code></pre>

FreeBSDでキーマップというとkeymap(5)やkbdcontrol(1)、そして/usr/share/syscons/<b>ファイルが関連するようです。 jp.106x.kbdを参考にしてjp.106.kbdをjp.106z.kbdにコピーして作業開始。</b>

jp.106.kbd:: 普通のキーマップjp.106x.kbd:: Caps LockをCtrlと入れ換えたもの<br>
<br>
なので<br>
<br>
jp.106z.kbd:: 全角半角をF10にするもの<br>
<br>
としました。<br>
<br>
以下jp.106.kbdとjp.106z.kbdの差分<br>
<br>
<pre><code>--- jp.106.kbd  Mon Jun  9 08:55:15 2003<br>
+++ jp.106z.kbd Sun May  9 16:23:41 2004<br>
@@ -1,5 +1,7 @@<br>
 # $FreeBSD: src/share/syscons/keymaps/jp.106.kbd,v 1.9 2001/03/11 23:41:18 ache Exp $<br>
 #                                                         alt<br>
+# (this one has zenkakuhankaku switch to F10)<br>
+#<br>
 # scan                       cntrl          alt    alt   cntrl lock<br>
 # code  base   shift  cntrl  shift  alt    shift  cntrl  shift state<br>
 # ------------------------------------------------------------------<br>
@@ -44,7 +46,7 @@<br>
   038   'l'    'L'    ff     ff     'l'    'L'    ff     ff      C<br>
   039   ';'    '+'    nop    nop    ';'    '+'    nop    nop     O<br>
   040   ':'    '*'    nop    nop    ':'    '*'    nop    nop     O<br>
-  041   esc    esc    esc    esc    esc    esc    debug  esc     O<br>
+  041   fkey10 fkey22 fkey34 fkey46 scr10  scr10  scr10  scr10   O<br>
   042   lshift lshift lshift lshift lshift lshift lshift lshift  O<br>
   043   ']'    '}'    gs     gs     ']'    '}'    gs     gs      O<br>
   044   'z'    'Z'    sub    sub    'z'    'Z'    sub    sub     C<br>
</code></pre>

068がF10のようだったのでこれを半角全角の041エントリにしました。<br>
<br>
<pre><code> 068   fkey10 fkey22 fkey34 fkey46 scr10  scr10  scr10  scr10   O<br>
</code></pre>

<a href='http://pc5.2ch.net/test/read.cgi/linux/1084073229/13-14'>http://pc5.2ch.net/test/read.cgi/linux/1084073229/13-14</a>

全角/半角キーをF10にマッピングできたら、~/.uimにこのように書けば全角/半角キーでオン/オフができるようになります。<br>
<br>
<pre><code>(define-key generic-on-key? '("zenkaku-hankaku" "&lt;Shift&gt; " "F10"))<br>
(define-key generic-off-key? '("zenkaku-hankaku" "&lt;Shift&gt; " "F10"))<br>
</code></pre>

<h4>w3mで使う</h4>

w3mでの日本語入力は一行入力だけです。 そこでw3mでの日本語入力は以下のようになってほしいと思います。 ここではIMの起動キーはCtrl+jとしていますが、好きなキーに変えることができます。<br>
<br>
<ol><li>一行入力のときにCtrl+jを押すとIMオン<br>
</li><li>一行入力が終わるとIMオフ<br>
</li><li>一行入力以外ではCtrl+jは他の機能</li></ol>

一行入力のときにCtrl+jでIMをオンにして、一行入力が終わったときにIMをオフにするにはw3mを改造する必要があります。<br>
<br>
<a href='http://sourceforge.net/projects/w3m/'>w3mのホームページ</a>からw3m-0.5.1.tar.gzをダウンロードします。 次に<a href='http://www.ice.nuie.nagoya-u.ac.jp/~h013177b/uim-fep/w3m-uim-fep.diff'>w3m-uim-fep.diff</a>をダウンロードします。<br>
<br>
<pre><code>*** linein.c.orig	2003-09-27 02:59:51.000000000 +0900<br>
--- linein.c	2004-05-20 18:32:36.000000000 +0900<br>
***************<br>
*** 49,60 ****<br>
  static void next_dcompl(int next);<br>
  static Str doComplete(Str ifn, int *status, int next);<br>
<br>
  /* *INDENT-OFF* */<br>
  void (*InputKeymap[32]) () = {<br>
  /*  C-@     C-a     C-b     C-c     C-d     C-e     C-f     C-g     */<br>
      _compl, _mvB,   _mvL,   _inbrk, delC,   _mvE,   _mvR,   _inbrk,<br>
  /*  C-h     C-i     C-j     C-k     C-l     C-m     C-n     C-o     */<br>
!     _bs,    iself,  _enter, killn,  iself,  _enter, _next,  _editor,<br>
  /*  C-p     C-q     C-r     C-s     C-t     C-u     C-v     C-w     */<br>
      _prev,  _quo,   _bsw,   iself,  _mvLw,  killb,  _quo,   _bsw,<br>
  /*  C-x     C-y     C-z     C-[     C-\     C-]     C-^     C-_     */<br>
--- 49,64 ----<br>
  static void next_dcompl(int next);<br>
  static Str doComplete(Str ifn, int *status, int next);<br>
<br>
+ static void im_set_mode(int mode);<br>
+ static void im_on();<br>
+ static void im_off();<br>
+<br>
  /* *INDENT-OFF* */<br>
  void (*InputKeymap[32]) () = {<br>
  /*  C-@     C-a     C-b     C-c     C-d     C-e     C-f     C-g     */<br>
      _compl, _mvB,   _mvL,   _inbrk, delC,   _mvE,   _mvR,   _inbrk,<br>
  /*  C-h     C-i     C-j     C-k     C-l     C-m     C-n     C-o     */<br>
!     _bs,    iself,  im_on, killn,  iself,  _enter, _next,  _editor,<br>
  /*  C-p     C-q     C-r     C-s     C-t     C-u     C-v     C-w     */<br>
      _prev,  _quo,   _bsw,   iself,  _mvLw,  killb,  _quo,   _bsw,<br>
  /*  C-x     C-y     C-z     C-[     C-\     C-]     C-^     C-_     */<br>
***************<br>
*** 255,260 ****<br>
--- 261,267 ----<br>
  	if (CLen &amp;&amp; (flag &amp; IN_CHAR))<br>
  	    break;<br>
      } while (i_cont);<br>
+     im_off();<br>
<br>
      if (CurrentTab) {<br>
  	if (need_redraw)<br>
***************<br>
*** 1133,1135 ****<br>
--- 1140,1168 ----<br>
      if (CurrentTab)<br>
  	displayBuffer(Currentbuf, B_FORCE_REDRAW);<br>
  }<br>
+<br>
+ static void<br>
+ im_set_mode(int mode)<br>
+ {<br>
+   char *setmode = getenv("UIM_FEP_SETMODE");<br>
+   if (setmode != NULL) {<br>
+     FILE *fp = fopen(setmode, "w");<br>
+     if (fp) {<br>
+       fprintf(fp, "%d\n", mode);<br>
+       fflush(fp);<br>
+       fclose(fp);<br>
+     }<br>
+   }<br>
+ }<br>
+<br>
+ static void<br>
+ im_on()<br>
+ {<br>
+   im_set_mode(1);<br>
+ }<br>
+<br>
+ static void<br>
+ im_off()<br>
+ {<br>
+   im_set_mode(0);<br>
+ }<br>
</code></pre>

w3mのソースにパッチを当ててコンパイル、インストールします。<br>
<br>
<pre><code>$ tar xvf w3m-0.5.1.tar.gz<br>
$ cd w3m-0.5.1<br>
$ patch &lt;../w3m-uim-fep.diff<br>
$ ./configure<br>
$ make<br>
# make install<br>
</code></pre>

一行入力以外のときのCtrl+jに機能を割り当てます。 例えばNEXT_DOWNを割り当てる場合は~/.w3m/keymapに次のように書きます。<br>
<br>
<pre><code>keymap C-j NEXT_DOWN<br>
</code></pre>

次に~/.uim-w3mを用意します。 ~/.uimに書いてしまうと、w3m以外でもCtrl+jでIMが起動しなくなってしまうので注意。<br>
<br>
<pre><code>;; uim-anthyの場合<br>
(define-key anthy-on-key? '())<br>
;; uim-skkの場合<br>
(define-key skk-on-key? '())<br>
;; uim-primeの場合<br>
(define-key prime-on-key? '())<br>
...<br>
</code></pre>

そして以下のような起動用スクリプトからw3mを起動します。<br>
<br>
<pre><code>#!/bin/sh<br>
# Ctrl+jとCtrl+mが区別させる<br>
stty -icrnl<br>
trap "stty icrnl" 0 1 2 3 15<br>
# w3mのパスは手元の環境に合わせてください<br>
LIBUIM_USER_SCM_FILE=~/.uim-w3m uim-fep -e /usr/local/bin/w3m "$@"<br>
</code></pre>

<h4>vimで使う</h4>

以下の方法より、<a href='http://yukihiro.nakadaira.googlepages.com/#uim-ctl'>uim-ctl</a>を使うほうがいいかもしれません。<br>
<br>
vim 6.4に<a href='http://www.kaoriya.net'>KaoriYaさん</a>のパッチを当てると、vimからuim-fepを制御できるようになります。 その他にもmigemoなどの便利な機能が使えるようになります。 ここではKaoriYaさんのパッチが6.4用のものであるとしてインストールの説明をします。<br>
<br>
cmigemoのインストール migemoを使わない場合はインストールする必要はありません。<br>
<br>
<pre><code>$ cvs -d :pserver:anonymous@cvs.kaoriya.net:/anonycvs login<br>
$ cvs -d :pserver:anonymous@cvs.kaoriya.net:/anonycvs checkout -r dev-1_3<br>
</code></pre>

migemo<br>
<br>
<pre><code>$ cd migemo<br>
$ ./configure<br>
$ make gcc<br>
$ make gcc-dict<br>
$ su<br>
# make gcc-install<br>
</code></pre>

ダウンロード <a href='http://www.vim.org'>vim.org</a>の<a href='http://www.vim.org/download.php'>ダウンロードのページ</a>から <a href='ftp://ftp.vim.org/pub/vim/unix/vim-6.4.tar.bz2'>vim-6.4.tar.bz2</a>、 <a href='ftp://ftp.vim.org/pub/vim/extra/vim-6.4-extra.tar.gz'>vim-6.4-extra.tar.gz</a>、 <a href='ftp://ftp.vim.org/pub/vim/extra/vim-6.4-lang.tar.gz'>vim-6.4-lang.tar.gz</a>、 <a href='http://www.kaoriya.net/#VIM64'>KaoriYaさん</a>からVim 6.4 差分パッケージをダウンロードします。<br>
<br>
<pre><code>$ wget ftp://ftp.vim.org/pub/vim/unix/vim-6.4.tar.bz2<br>
$ wget ftp://ftp.vim.org/pub/vim/extra/vim-6.4-extra.tar.gz<br>
$ wget ftp://ftp.vim.org/pub/vim/extra/vim-6.4-lang.tar.gz<br>
$ wget http://www.kaoriya.net/dist/vim-6.4-difj.tar.bz2<br>
</code></pre>

コンパイル 展開します。<br>
<br>
<pre><code>$ tar jxvf vim-6.4-difj.tar.bz2<br>
$ tar jxvf vim-6.4.tar.bz2<br>
$ tar zxvf vim-6.4-extra.tar.gz<br>
$ tar zxvf vim-6.4-lang.tar.gz<br>
</code></pre>

gnu tarがない場合は<br>
<br>
<pre><code>$ bunzip2 -c vim-6.4-difj.tar.bz2|tar xvf -<br>
$ bunzip2 -c vim-6.4.tar.bz2|tar xvf -<br>
$ gunzip -c vim-6.4-extra.tar.gz|tar xvf -<br>
$ gunzip -c vim-6.4-lang.tar.gz|tar xvf -<br>
</code></pre>

パッチを当ててconfigureします。<br>
<br>
<pre><code>$ cd vim64<br>
$ patch -p0 &lt;../vim-6.4-difj/diffs/kaoriya.diff<br>
$ ./configure --with-features=big --enable-multibyte<br>
</code></pre>

あとはmakeするだけです。<br>
<br>
<pre><code>$ make<br>
$ su<br>
# make install<br>
</code></pre>

必要な設定<br>
<br>
<pre><code>:set ttimeoutlen=10<br>
</code></pre>

操作方法 インサートモードでCtrl+<sup>を押すとIMがオンになります。 IMがオンの状態で、Ctrl+</sup>を押すとIMがオフになります。 Escを押してノーマルモードになるとIMは自動的にオフになります。 再度インサートモードにすると、以前のインサートモードのIMの状態に戻ります。<br>
<br>
キーバインドの変更 IMをオンにするキーを変更する方法です。 例えばCtrl+jにするには~/.vimrcで以下のように設定します。<br>
<br>
<pre><code>:inoremap &lt;C-j&gt; &lt;C-^&gt;<br>
:cnoremap &lt;C-j&gt; &lt;C-^&gt;<br>
</code></pre>

ただし、cnoremapで<br>
<br>
<C-j><br>
<br>
にマップすると、@:を押すとIMがオンになってしまい、前回のexコマンドを繰り返せなくなります。<br>
<br>
uimの方は以下のように設定します。 skkのF10は全角英数モードになったときにひらがなモードに戻すためです。<br>
<br>
<pre><code>(define-key skk-on-key? '("F10"))<br>
(define-key anthy-on-key? '())<br>
(define-key prime-on-key? '())<br>
</code></pre>

IMの状態を保存しない インサートモードになったときに常にIMがオフになるようにする方法です。 ただし、インサートモードで矢印キーなどが効かなくなります。<br>
<br>
<pre><code>:inoremap &lt;silent&gt; &lt;esc&gt; &lt;esc&gt;:se imi=0&lt;cr&gt;<br>
</code></pre>

デフォルトでIMをオフにする vimを起動して最初にインサートモードになったときにIMをオフにする方法です。<br>
<br>
<pre><code>:se imi=0<br>
:se ims=0<br>
</code></pre>

パッチを当てる ノーマルモードのfコマンドでIMがオンになったりするなど使いにくいところがあっ たのでパッチを作りました。<br>
<br>
f, F, t, T, rでIMをオンにしない IMをオンにした状態でノーマルモードになってfなどを押すとIMがオンになっ てしまいます。これを回避するためのパッチです。 <a href='http://www.ice.nuie.nagoya-u.ac.jp/~h013177b/uim-fep/uim-fep-vim-fFtTr-6.3.054.diff'>6.3.054用</a> <a href='http://www.ice.nuie.nagoya-u.ac.jp/~h013177b/uim-fep/uim-fep-vim-fFtTr-6.3.085.diff'>6.3.085用</a> <a href='http://www.ice.nuie.nagoya-u.ac.jp/~h013177b/uim-fep/uim-fep-vim-fFtTr-6.4.diff'>6.4用</a>

<C-<sup>>でIMをオフにしない <C-</sup>>はIMをトグルするキーですが、<C-^>でIMをオフにしないようにするため のパッチです。IMをオフにするときはuimのキーバインドで行います。 <a href='http://www.ice.nuie.nagoya-u.ac.jp/~h013177b/uim-fep/uim-fep-vim-hat-6.3.054.diff'>6.3.054用</a> <a href='http://www.ice.nuie.nagoya-u.ac.jp/~h013177b/uim-fep/uim-fep-vim-hat-6.3.085.diff'>6.3.085用</a> <a href='http://www.ice.nuie.nagoya-u.ac.jp/~h013177b/uim-fep/uim-fep-vim-hat-6.4.diff'>6.4用</a>

/(検索)のときにIMをオンにしない /や?で検索するときにIMをオフにするパッチです。 <a href='http://www.ice.nuie.nagoya-u.ac.jp/~h013177b/uim-fep/uim-fep-vim-search-6.3.054.diff'>6.3.054用</a> <a href='http://www.ice.nuie.nagoya-u.ac.jp/~h013177b/uim-fep/uim-fep-vim-search-6.3.085.diff'>6.3.085用</a> <a href='http://www.ice.nuie.nagoya-u.ac.jp/~h013177b/uim-fep/uim-fep-vim-search-6.4.diff'>6.4用</a>

<C-^>で常にひらがなモードにする skkでは全角英数からIMをオフにして再度オンにすると全角英数になってしまいます。 IMがオンになったときは常にひらがなモードにするためのパッチです。 <a href='http://www.ice.nuie.nagoya-u.ac.jp/~h013177b/uim-fep/uim-fep-vim-hiragana-6.3.054.diff'>6.3.054用</a> <a href='http://www.ice.nuie.nagoya-u.ac.jp/~h013177b/uim-fep/uim-fep-vim-hiragana-6.3.085.diff'>6.3.085用</a> <a href='http://www.ice.nuie.nagoya-u.ac.jp/~h013177b/uim-fep/uim-fep-vim-hiragana-6.4.diff'>6.4用</a>

@:でIMがオンにならないようにする cnoremapで<br>
<br>
<C-j><br>
<br>
にマップしていると、@:が効かなくなるのを回避するためのパッチです。 <a href='http://www.ice.nuie.nagoya-u.ac.jp/~h013177b/uim-fep/uim-fep-vim-nlmap-6.3.054.diff'>6.3.054用</a> <a href='http://www.ice.nuie.nagoya-u.ac.jp/~h013177b/uim-fep/uim-fep-vim-nlmap-6.3.085.diff'>6.3.085用</a> <a href='http://www.ice.nuie.nagoya-u.ac.jp/~h013177b/uim-fep/uim-fep-vim-nlmap-6.4.diff'>6.4用</a>

パッチの当て方 KaoriYaパッチを当てたあとにvim64ディレクトリで、このように当てます。<br>
<br>
<pre><code>$for i in uim-fep-vim-*.diff<br>
 do<br>
   patch -p0 &lt; $i<br>
 done<br>
</code></pre>

上の5つのパッチを全部当てる場合は5つのパッチをまとめたこのパッチを使ってください。 <a href='http://www.ice.nuie.nagoya-u.ac.jp/~h013177b/uim-fep/uim-fep-vim-all-6.3.054.diff'>6.3.054用</a> <a href='http://www.ice.nuie.nagoya-u.ac.jp/~h013177b/uim-fep/uim-fep-vim-all-6.3.085.diff'>6.3.085用</a> <a href='http://www.ice.nuie.nagoya-u.ac.jp/~h013177b/uim-fep/uim-fep-vim-all-6.4.diff'>6.4用</a>

起動スクリプト<br>
<br>
<pre><code>#!/bin/sh<br>
LIBUIM_USER_SCM_FILE=~/.uim-vim exec uim-fep -e /usr/local/bin/vim "$@"<br>
</code></pre>

この起動スクリプトをvimという名前にする場合は最後の行の-eの後のvimを本物の vimのフルパスにしてください。<br>
<br>
<h3>UimEl uim.el</h3>

<h4>IMのON/OFFでカーソルの色を変化させる</h4>

<a href='http://d.hatena.ne.jp/higepon/20061002/1159797987'>http://d.hatena.ne.jp/higepon/20061002/1159797987</a>

<pre><code>;; uim-mode by higepon<br>
;; ON/OFFでカーソルの色を変更。<br>
;; ON時に必ず日本語入力モードにする<br>
(defadvice uim-this-command-keys (around uim-send-zenkaku-hankaku)<br>
  (setq ad-return-value `[zenkaku-hankaku]))<br>
(defadvice uim-mode (around my-uim-mode)<br>
  ad-do-it<br>
  (set-face-background 'cursor (if ad-return-value "blue" "indian red"))<br>
  (ad-activate-regexp "uim-send-zenkaku-hankaku")<br>
  (uim-process-input)<br>
  (ad-deactivate-regexp "uim-send-zenkaku-hankaku"))<br>
(ad-activate-regexp "my-uim-mode")<br>
</code></pre>

<h3>その他</h3>

<h4>編集領域の配色を独自配色に</h4>

基本的な書式<br>
<br>
<pre><code>(require "util.scm")<br>
(define uim-color-配色名<br>
  '((変数 . 値)<br>
...<br>
    (変数 . 値)))<br>
(define uim-color 'uim-color-配色名)<br>
</code></pre>

<pre><code>; 例<br>
(require "util.scm")<br>
(define uim-color-mono<br>
  '((reversed-preedit-foreground   . "white")<br>
    (reversed-preedit-background   . "black")<br>
    (separator-foreground          . "white")<br>
    (separator-background          . "black")<br>
    (reversed-separator-foreground . "white")<br>
    (reversed-separator-background . "black")))<br>
(define uim-color 'uim-color-mono)<br>
</code></pre>

<table><thead><th> 動作 </th><th> 変数名 </th><th> 指定できる値 </th></thead><tbody>
<tr><td>    </td><td> reversed-preedit-foreground </td><td> "色名"   </td></tr>
<tr><td>    </td><td> reversed-preedit-background </td><td> "色名"   </td></tr>
<tr><td>    </td><td> separator-foreground </td><td> "色名"   </td></tr>
<tr><td>    </td><td> separator-background </td><td> "色名"   </td></tr>
<tr><td>    </td><td> reversed-separator-foreground </td><td> "色名"   </td></tr>
<tr><td>    </td><td> reversed-separator-background </td><td> "色名"   </td></tr></tbody></table>

<h4>IMそれぞれにIM切り換えキーを割り当てる</h4>

<a href='http://groups.google.com/group/uim-en/t/b64641ed041ea9a6'>http://groups.google.com/group/uim-en/t/b64641ed041ea9a6</a>

$prefix/share/uim/im.scmを<br>
<br>
<pre><code>Index: im.scm<br>
===================================================================<br>
--- im.scm      (revision 5780)<br>
+++ im.scm      (working copy)<br>
@@ -456,6 +456,15 @@<br>
        ((and enable-im-switch?<br>
             (switch-im-key? key state))<br>
        (switch-im uc (im-name im)))<br>
+<br>
+       ;; im switch hack<br>
+       ((switch-to-im1-key? key state)<br>
+       (im-switch-im uc switch-im1))<br>
+       ((switch-to-im2-key? key state)<br>
+       (im-switch-im uc switch-im2))<br>
+       ((switch-to-im3-key? key state)<br>
+       (im-switch-im uc switch-im3))<br>
+<br>
        ((modifier-key? key state)<br>
        ;; don't discard modifier press/release edge for apps<br>
        (im-commit-raw c))<br>
</code></pre>

~/.uimに<br>
<br>
<pre><code>(define switch-to-im1-key '("&lt;Alt&gt;1"))<br>
(define switch-to-im1-key? (make-key-predicate switch-to-im1-key))<br>
(define switch-im1 'direct)<br>
<br>
(define switch-to-im2-key '("&lt;Alt&gt;2"))<br>
(define switch-to-im2-key? (make-key-predicate switch-to-im2-key))<br>
(define switch-im2 'm17n-ru-kbd)<br>
<br>
(define switch-to-im3-key '("&lt;Alt&gt;3"))<br>
(define switch-to-im3-key? (make-key-predicate switch-to-im3-key))<br>
(define switch-im3 'anthy)<br>
</code></pre>

この例では、Alt+1で直接入力、Alt+2でm17n-ru-kbd、Alt+3でAnthyに切り換わります。<br>
<br>
<h4>uimに新しいモジュールを追加する</h4>

uimアーカイブには含まれていないモジュールが色々と公開されています。 どんなモジュールがあるかは、<a href='UimLinks.md'>UimLinks</a>ページの「関係ソフトウェア」の項をどうぞ。<br>
<br>
幾つか注意点あります。<br>
<br>
インストール先に注意してください。 uimが/usr/lib下にインストールされているなら、モジュールも/usr/lib下にインストールする必要があります。<br>
<br>
インストールが完了したら、<a href='UimModuleManager.md'>UimModuleManager</a>でuimのモジュールリストへ追加してください。 例えばuim-festivalモジュールを追加するには<br>
<br>
<pre><code># uim-module-manager --register festival<br>
</code></pre>

後は<a href='UimPref.md'>UimPref</a>で「使用可能にする入力方式」の有効リストに入れましょう。<br>
<br>
<h2>変換用テーブルのカスタマイズ</h2>

<h3>RomaKanaTable ローマ字入力方式</h3>

基本的な書式 (for uim >= 1.6)<br>
<br>
<pre><code>(require "japanese.scm")<br>
(set! ja-rk-rule-basic (cons '(<br>
  (("キー名") . ()) ("ひらがな入力モード" "カタカナ入力モード" "半角カタカナ入力モード")<br>
 )<br>
ja-rk-rule-basic))<br>
(ja-rk-rule-update)<br>
</code></pre>

<pre><code>(require "japanese.scm")<br>
(define ja-rk-rule-basic (append '(<br>
  ((("キー名") . ()) ("ひらがな入力モード" "カタカナ入力モード" "半角カタカナ入力モード"))<br>
...<br>
   ((("キー名") . ()) ("ひらがな入力モード" "カタカナ入力モード" "半角カタカナ入力モード")))<br>
  ja-rk-rule-basic))<br>
(ja-rk-rule-update)<br>
</code></pre>

<a href='UimSkk.md'>uim-skk</a>では、ja-rk-ruleではなくskk-ja-rk-ruleが使用されるため、<br>
上記の設定をした後に、<br>
<pre><code>(define skk-ja-rk-rule (append ja-rk-rule-basic ja-rk-rule-additional)<br>
</code></pre>
を設定。<br>
<br>
<br>
スペースには''ja-space''と''ja-alnum-space''という専用の変数が用意されている。<br>
<br>
<pre><code>(require "japanese.scm")<br>
(define ja-space '("ひらがな入力モード "カタカナ入力モード" "半角カタカナ入力モード"))<br>
(define ja-alnum-space '("半角英数入力モード" "全角英数入力モード"))<br>
</code></pre>

入力後、即座に確定するキーは''ja-direct-rule''という変数を使う。<br>
<br>
<pre><code>(require "japanese.scm")<br>
(set! ja-direct-rule (cons '(<br>
 ("キー名" "文字")<br>
 )<br>
ja-direct-rule))<br>
</code></pre>

としてください。<br>
<br>
<h4>余分な変換ルールを無効にしたい</h4>

変換用テーブルは、基礎的なテーブルの'''ja-rk-rule-basic'''と、付加的なテーブルの'''ja-rk-rule-additional'''に分かれています。 ja-rk-rule-additionalを使わないように設定することで、一風変わった変換ルールをまとめて無効にできます。<br>
<br>
<pre><code>(require "japanese.scm")<br>
(define ja-rk-rule-update<br>
  (lambda ()<br>
    (if ja-rk-rule-keep-consonant?<br>
      (set! ja-rk-rule (append ja-rk-rule-consonant-to-keep<br>
                               ja-rk-rule-basic))<br>
      (set! ja-rk-rule ja-rk-rule-basic))))<br>
(ja-rk-rule-update)<br>
</code></pre>

<h4>「。」を「．」、「、」を「，」としたい</h4>

<pre><code>(require "japanese.scm")<br>
(define ja-rk-rule-basic<br>
  (append '(<br>
            (((",") . ()) ("，" "，" "，"))<br>
            (((".") . ()) ("．" "．" "．"))<br>
            )<br>
          ja-rk-rule-basic))<br>
(ja-rk-rule-update)<br>
</code></pre>

<h4>「／」を「・」、「＼」を「￥」としたい</h4>

<pre><code>(require "japanese.scm")<br>
(define ja-rk-rule-basic<br>
  (append '(<br>
            ((("/") . ()) ("・" "・" "・"))<br>
            ((("\\") . ()) ("￥" "￥" "￥"))<br>
            )<br>
          ja-rk-rule-basic))<br>
(ja-rk-rule-update)<br>
</code></pre>

<h4>"z SPC"で全角スペースを入力する</h4>

'''これは<a href='UimSkk.md'>UimSkk</a>でのみ有効です。'''<br>
<br>
<pre><code>(require-module "skk")<br>
(define skk-ja-rk-rule<br>
  (append '(<br>
    ((("z" " "). ())("　" "　" "　"))<br>
    )<br>
  skk-ja-rk-rule))<br>
</code></pre>

<h4>MS-IME風ローマ字配列</h4>

<pre><code>(require "japanese.scm")<br>
(define ja-rk-rule-basic<br>
  (append '(<br>
            ((("c" "a"). ())("か" "カ" "ｶ"))<br>
            ((("c" "i"). ())("し" "シ" "ｼ"))<br>
            ((("c" "u"). ())("く" "ク" "ｸ"))<br>
            ((("c" "e"). ())("せ" "セ" "ｾ"))<br>
            ((("c" "o"). ())("そ" "ソ" "ｿ"))<br>
            ((("q" "q"). ("q"))("っ" "ッ" "ｯ"))<br>
            ((("v" "y" "i"). ())(("う゛" "ヴ" "ｳﾞ") ("ぃ" "ィ" "ｨ")))<br>
            ((("x" "n"). ())("ん" "ン" "ﾝ"))<br>
            ((("x" "x"). ("x"))("っ" "ッ" "ｯ"))<br>
            )<br>
          ja-rk-rule-basic))<br>
(ja-rk-rule-update)<br>
</code></pre>

<h4>ATOK風ローマ字配列</h4>

<pre><code>(require "japanese.scm")<br>
(define ja-rk-rule-basic<br>
  (append '(<br>
            ((("l" "k" "a"). ())("ヵ" "ヵ" "ｶ"))<br>
            ((("l" "k" "e"). ())("ヶ" "ヶ" "ｹ"))<br>
            ((("l" "w" "a"). ())("ゎ" "ヮ" "ﾜ"))<br>
            )<br>
          ja-rk-rule-basic))<br>
(ja-rk-rule-update)<br>
</code></pre>

<h4>Wnn風ローマ字配列</h4>

<pre><code>(require "japanese.scm")<br>
(define ja-rk-rule-basic<br>
  (append '(<br>
            ((("\\" "a"). ())("ぁ" "ァ" "ｧ"))<br>
            ((("\\" "i"). ())("ぃ" "ィ" "ｨ"))<br>
            ((("\\" "u"). ())("ぅ" "ゥ" "ｩ"))<br>
            ((("\\" "e"). ())("ぇ" "ェ" "ｪ"))<br>
            ((("\\" "o"). ())("ぉ" "ォ" "ｫ"))<br>
            ((("\\" "k" "a"). ())("ヵ" "ヵ" "ｶ"))<br>
            ((("\\" "k" "e"). ())("ヶ" "ヶ" "ｹ"))<br>
            ((("\\" "y" "a"). ())("ゃ" "ャ" "ｬ"))<br>
            ((("\\" "y" "u"). ())("ゅ" "ュ" "ｭ"))<br>
            ((("\\" "y" "o"). ())("ょ" "ョ" "ｮ"))<br>
            ((("g" "w" "a"). ())(("ぐ" "グ" "ｸﾞ") ("ゎ" "ヮ" "ﾜ")))<br>
            ((("g" "w" "u"). ())("ぐ" "グ" "ｸﾞ"))<br>
            ((("k" "w" "a"). ())(("く" "ク" "ｸ") ("ゎ" "ヮ" "ﾜ")))<br>
            ((("k" "w" "u"). ())("く" "ク" "ｸ"))<br>
            ((("l" "a"). ())("ら" "ラ" "ﾗ"))<br>
            ((("l" "i"). ())("り" "リ" "ﾘ"))<br>
            ((("l" "u"). ())("る" "ル" "ﾙ"))<br>
            ((("l" "e"). ())("れ" "レ" "ﾚ"))<br>
            ((("l" "o"). ())("ろ" "ロ" "ﾛ"))<br>
            ((("m" "m"). ("m"))("ん" "ン" "ﾝ"))<br>
            ((("n" "'"). ())("ん" "ン" "ﾝ"))<br>
            ((("t" "c" "h"). ("h" "c"))("っ" "ッ" "ｯ"))<br>
            ((("t" "s" "a"). ())(("つ" "ツ" "ﾂ") ("ぁ" "ァ" "ｧ")))<br>
            ((("t" "s" "i"). ())(("つ" "ツ" "ﾂ") ("ぃ" "ィ" "ｨ")))<br>
            ((("t" "s" "e"). ())(("つ" "ツ" "ﾂ") ("ぇ" "ェ" "ｪ")))<br>
            ((("t" "s" "o"). ())(("つ" "ツ" "ﾂ") ("ぉ" "ォ" "ｫ")))<br>
            ((("w" "i"). ())("ゐ" "ヰ" "ｨ"))<br>
            ((("w" "e"). ())("ゑ" "ヱ" "ｪ"))<br>
            ((("x" "/"). ())("/" "/" "/"))<br>
            ((("x" "-"). ())("-" "-" "-"))<br>
            ((("x" ","). ())("," "," ","))<br>
            ((("x" "."). ())("." "." "."))<br>
            ((("x" "~"). ())("~" "~" "~"))<br>
            ((("x" "^"). ())("^" "^" "^"))<br>
            ((("x" "\\"). ())("＼" "＼" "\\"))<br>
            ((("x" "["). ())("[" "[" "["))<br>
            ((("x" ";"). ())(";" ";" ";"))<br>
            ((("x" ":"). ())(":" ":" ":"))<br>
            ((("x" "]"). ())("]" "]" "]"))<br>
            ((("x" "/"). ())("/" "/" "/"))<br>
            ((("x" "d" "i"). ())(("で" "デ" "ﾃﾞ") ("ぃ" "ィ" "ｨ")))<br>
            ((("x" "d" "u"). ())(("ど" "ド" "ﾄﾞ") ("ぅ" "ゥ" "ｩ")))<br>
            ((("x" "d" "e"). ())(("で" "デ" "ﾃﾞ") ("ぇ" "ェ" "ｪ")))<br>
            ((("x" "d" "o"). ())(("ど" "ド" "ﾄﾞ") ("ぉ" "ォ" "ｫ")))<br>
            ((("x" "t" "i"). ())(("て" "テ" "ﾃ") ("ぃ" "ィ" "ｨ")))<br>
            ((("x" "w" "i"). ())(("う" "ウ" "ｳ") ("ぃ" "ィ" "ｨ")))<br>
            ((("x" "w" "e"). ())(("う" "ウ" "ｳ") ("ぇ" "ェ" "ｪ")))<br>
            ((("x" "w" "o"). ())(("う" "ウ" "ｳ") ("ぉ" "ォ" "ｫ")))<br>
            )<br>
          ja-rk-rule-basic))<br>
(ja-rk-rule-update)<br>
</code></pre>

<h4>Canna風ローマ字配列</h4>

<pre><code>(require "japanese.scm")<br>
(define ja-rk-rule-basic<br>
  (append '(<br>
            ((("\\"). ())("￥" "￥" "\\"))<br>
            ((("{"). ())("『" "『" "["))<br>
            ((("}"). ())("』" "』" "]"))<br>
            ((("@" "-"). ("/"))("-" "-" "-"))<br>
            ((("@" "/"). ())("・" "・" "･"))<br>
            ((("@" "\\"). ())("＼" "＼" "\\"))<br>
            ((("@" ","). ())("，" "，" ","))<br>
            ((("@" "."). ())("．" "．" "."))<br>
            ((("@" "~"). ())("〜" "〜" "~"))<br>
            ((("@" "|" "|"). ())("‖" "‖" ""))<br>
            ((("@" "|"). ())("｜" "｜" "|"))<br>
            ((("@" "3"). ())("…" "…" ""))<br>
            ((("@" "2"). ())("‥" "‥" ""))<br>
            ((("@" "("). ())("（" "（" "("))<br>
            ((("@" ")"). ())("）" "）" ")"))<br>
            ((("@" "["). ())("［" "［" "["))<br>
            ((("@" "]"). ())("］" "］" "]"))<br>
            ((("@" "{"). ())("｛" "｛" "{"))<br>
            ((("@" "}"). ())("｝" "｝" "}"))<br>
            ((("c" "a"). ())("か" "カ" "ｶ"))<br>
            ((("c" "u"). ())("く" "ク" "ｸ"))<br>
            ((("c" "o"). ())("こ" "コ" "ｺ"))<br>
            ((("l" "a"). ())("ら" "ラ" "ﾗ"))<br>
            ((("l" "i"). ())("り" "リ" "ﾘ"))<br>
            ((("l" "u"). ())("る" "ル" "ﾙ"))<br>
            ((("l" "e"). ())("れ" "レ" "ﾚ"))<br>
            ((("l" "o"). ())("ろ" "ロ" "ﾛ"))<br>
            ((("m" "n"). ())("ん" "ン" "ﾝ"))<br>
            ((("n" "'"). ())("ん" "ン" "ﾝ"))<br>
            ((("q" "q"). ("q"))("っ" "ッ" "ｯ"))<br>
            ((("t" "c" "h"). ("h" "c"))("っ" "ッ" "ｯ"))<br>
            ((("w" "i"). ())("ゐ" "ヰ" "ｨ"))<br>
            ((("w" "e"). ())("ゑ" "ヱ" "ｪ"))<br>
            )<br>
          ja-rk-rule-basic))<br>
(ja-rk-rule-update)<br>
</code></pre>

<h4>VJE風ローマ字配列</h4>

<pre><code>(require "japanese.scm")<br>
(define ja-rk-rule-basic<br>
  (append '(<br>
            ((("c" "a"). ())("か" "カ" "ｶ"))<br>
            ((("c" "i"). ())("し" "シ" "ｼ"))<br>
            ((("c" "u"). ())(("き" "キ" "ｷ") ("ゅ" "ュ" "ｭ")))<br>
            ((("c" "e"). ())("せ" "セ" "ｾ"))<br>
            ((("c" "o"). ())("そ" "ソ" "ｿ"))<br>
            ((("g" "w" "a"). ())(("ぐ" "グ" "ｸﾞ") ("ゎ" "ヮ" "ﾜ")))<br>
            ((("g" "w" "u"). ())("ぐ" "グ" "ｸﾞ"))<br>
            ((("k" "w" "a"). ())(("く" "ク" "ｸ") ("ゎ" "ヮ" "ﾜ")))<br>
            ((("k" "w" "u"). ())("く" "ク" "ｸ"))<br>
            ((("l" "a"). ())("ら" "ラ" "ﾗ"))<br>
            ((("l" "i"). ())("り" "リ" "ﾘ"))<br>
            ((("l" "u"). ())("る" "ル" "ﾙ"))<br>
            ((("l" "e"). ())("れ" "レ" "ﾚ"))<br>
            ((("l" "o"). ())("ろ" "ロ" "ﾛ"))<br>
            ((("q" "a"). ())(("く" "ク" "ｸ") ("ぁ" "ァ" "ｧ")))<br>
            ((("q" "i"). ())(("く" "ク" "ｸ") ("ぃ" "ィ" "ｨ")))<br>
            ((("q" "u"). ())("く" "ク" "ｸ"))<br>
            ((("q" "e"). ())(("く" "ク" "ｸ") ("ぇ" "ェ" "ｪ")))<br>
            ((("q" "o"). ())(("く" "ク" "ｸ") ("ぉ" "ォ" "ｫ")))<br>
            ((("x" "x"). ("x"))("っ" "ッ" "ｯ"))<br>
            )<br>
          ja-rk-rule-basic))<br>
(ja-rk-rule-update)<br>
</code></pre>

<h4>Egg風ローマ字配列</h4>

<a href='ftp://ftp.linet.gr.jp/pub/Plamo/Plamo-4.2/contrib/FEP/'>ftp://ftp.linet.gr.jp/pub/Plamo/Plamo-4.2/contrib/FEP/</a>

<pre><code>(require "japanese.scm")<br>
(define ja-rk-rule-basic<br>
  (append '(<br>
            ((("g" "s" "e"). ())(("つ" "ツ" "ﾂ") ("ぇ" "ェ" "ｪ")))<br>
            ((("g" "w" "u"). ())("ぐ" "グ" "ｸﾞ"))<br>
            ((("k" "w" "u"). ())("く" "ク" "ｸ"))<br>
            ((("l" "a"). ())("ら" "ラ" "ﾗ"))<br>
            ((("l" "i"). ())("り" "リ" "ﾘ"))<br>
            ((("l" "u"). ())("る" "ル" "ﾙ"))<br>
            ((("l" "e"). ())("れ" "レ" "ﾚ"))<br>
            ((("l" "o"). ())("ろ" "ロ" "ﾛ"))<br>
            ((("n" "'"). ())("ん" "ン" "ﾝ"))<br>
            ((("w" "i"). ())("ゐ" "ヰ" "ｨ"))<br>
            ((("w" "e"). ())("ゑ" "ヱ" "ｪ"))<br>
            ((("x" "d" "i"). ())(("で" "デ" "ﾃﾞ") ("ぃ" "ィ" "ｨ")))<br>
            ((("x" "d" "u"). ())(("ど" "ド" "ﾄﾞ") ("ぅ" "ゥ" "ｩ")))<br>
            ((("x" "d" "e"). ())(("で" "デ" "ﾃﾞ") ("ぇ" "ェ" "ｪ")))<br>
            ((("x" "d" "o"). ())(("ど" "ド" "ﾄﾞ") ("ぉ" "ォ" "ｫ")))<br>
            ((("x" "t" "i"). ())(("て" "テ" "ﾃ") ("ぃ" "ィ" "ｨ")))<br>
            ((("x" "w" "i"). ())(("う" "ウ" "ｳ") ("ぃ" "ィ" "ｨ")))<br>
            ((("x" "w" "e"). ())(("う" "ウ" "ｳ") ("ぇ" "ェ" "ｪ")))<br>
            ((("x" "w" "o"). ())(("う" "ウ" "ｳ") ("ぉ" "ォ" "ｫ")))<br>
            ((("z" "!"). ())("●" "●" ""))<br>
            ((("z" "\""). ())("“" "“" ""))<br>
            ((("z" "#"). ())("▲" "▲" ""))<br>
            ((("z" "$"). ())("■" "■" ""))<br>
            ((("z" "&amp;"). ())("£" "£" ""))<br>
            ((("z" "'"). ())("‘" "‘" ""))<br>
            ((("z" "("). ())("【" "【" ""))<br>
            ((("z" ")"). ())("】" "】" ""))<br>
            ((("z" "~"). ())("¨" "¨" ""))<br>
            ((("z" "="). ())("≠" "≠" ""))<br>
            ((("z" "^"). ())("★" "★" ""))<br>
            ((("z" "\\"). ())("＼" "＼" ""))<br>
            ((("z" "|"). ())("‖" "‖" ""))<br>
            ((("z" "`"). ())("´" "´" ""))<br>
            ((("z" "@"). ())("▼" "▼" ""))<br>
            ((("z" "{"). ())("〔" "〔" ""))<br>
            ((("z" "+"). ())("±" "±" ""))<br>
            ((("z" ";"). ())("゛" "゛" ""))<br>
            ((("z" "*"). ())("×" "×" ""))<br>
            ((("z" ":"). ())("゜" "゜" ""))<br>
            ((("z" "}"). ())("〕" "〕" ""))<br>
            ((("z" "&lt;"). ())("≦" "≦" ""))<br>
            ((("z" "&gt;"). ())("≧" "≧" ""))<br>
            ((("z" "?"). ())("∞" "∞" ""))<br>
            ((("z" "_"). ())("∴" "∴" ""))<br>
            ((("z" "1"). ())("○" "○" ""))<br>
            ((("z" "2"). ())("▽" "▽" ""))<br>
            ((("z" "3"). ())("△" "△" ""))<br>
            ((("z" "4"). ())("□" "□" ""))<br>
            ((("z" "5"). ())("◇" "◇" ""))<br>
            ((("z" "6"). ())("☆" "☆" ""))<br>
            ((("z" "7"). ())("◎" "◎" ""))<br>
            ((("z" "8"). ())("¢" "¢" ""))<br>
            ((("z" "9"). ())("♂" "♂" ""))<br>
            ((("z" "0"). ())("♀" "♀" ""))<br>
            ((("z" "b"). ())("°" "°" ""))<br>
            ((("z" "c"). ())("〇" "〇" ""))<br>
            ((("z" "d"). ())("ゝ" "ゝ" ""))<br>
            ((("z" "f"). ())("〃" "〃" ""))<br>
            ((("z" "g"). ())("‐" "‐" ""))<br>
            ((("z" "m"). ())("″" "″" ""))<br>
            ((("z" "n"). ())("′" "′" ""))<br>
            ((("z" "p"). ())("〒" "〒" ""))<br>
            ((("z" "q"). ())("《" "《" ""))<br>
            ((("z" "r"). ())("々" "々" ""))<br>
            ((("z" "s"). ())("ヽ" "ヽ" ""))<br>
            ((("z" "t"). ())("〆" "〆" ""))<br>
            ((("z" "v"). ())("※" "※" ""))<br>
            ((("z" "w"). ())("》" "》" ""))<br>
            ((("z" "x"). ())((":" ":" "") ("-" "-" "")))<br>
            ((("z" "B"). ())("←" "←" ""))<br>
            ((("z" "C"). ())("℃" "℃" ""))<br>
            ((("z" "D"). ())("ゞ" "ゞ" ""))<br>
            ((("z" "F"). ())("→" "→" ""))<br>
            ((("z" "G"). ())("―" "―" ""))<br>
            ((("z" "M"). ())("〓" "〓" ""))<br>
            ((("z" "N"). ())("↓" "↓" ""))<br>
            ((("z" "P"). ())("↑" "↑" ""))<br>
            ((("z" "Q"). ())("〈" "〈" ""))<br>
            ((("z" "R"). ())("仝" "仝" ""))<br>
            ((("z" "S"). ())("ヾ" "ヾ" ""))<br>
            ((("z" "T"). ())("§" "§" ""))<br>
            ((("z" "V"). ())("÷" "÷" ""))<br>
            ((("z" "W"). ())("〉" "〉" ""))<br>
            ((("Z" "a"). ())("ａ" "ａ" ""))<br>
            ((("Z" "b"). ())("ｂ" "ｂ" ""))<br>
            ((("Z" "c"). ())("ｃ" "ｃ" ""))<br>
            ((("Z" "d"). ())("ｄ" "ｄ" ""))<br>
            ((("Z" "e"). ())("ｅ" "ｅ" ""))<br>
            ((("Z" "f"). ())("ｆ" "ｆ" ""))<br>
            ((("Z" "g"). ())("ｇ" "ｇ" ""))<br>
            ((("Z" "h"). ())("ｈ" "ｈ" ""))<br>
            ((("Z" "i"). ())("ｉ" "ｉ" ""))<br>
            ((("Z" "j"). ())("ｊ" "ｊ" ""))<br>
            ((("Z" "k"). ())("ｋ" "ｋ" ""))<br>
            ((("Z" "l"). ())("ｌ" "ｌ" ""))<br>
            ((("Z" "m"). ())("ｍ" "ｍ" ""))<br>
            ((("Z" "n"). ())("ｎ" "ｎ" ""))<br>
            ((("Z" "o"). ())("ｏ" "ｏ" ""))<br>
            ((("Z" "p"). ())("ｐ" "ｐ" ""))<br>
            ((("Z" "q"). ())("ｑ" "ｑ" ""))<br>
            ((("Z" "r"). ())("ｒ" "ｒ" ""))<br>
            ((("Z" "s"). ())("ｓ" "ｓ" ""))<br>
            ((("Z" "t"). ())("ｔ" "ｔ" ""))<br>
            ((("Z" "u"). ())("ｕ" "ｕ" ""))<br>
            ((("Z" "v"). ())("ｖ" "ｖ" ""))<br>
            ((("Z" "w"). ())("ｗ" "ｗ" ""))<br>
            ((("Z" "x"). ())("ｘ" "ｘ" ""))<br>
            ((("Z" "y"). ())("ｙ" "ｙ" ""))<br>
            ((("Z" "z"). ())("ｚ" "ｚ" ""))<br>
            )<br>
          ja-rk-rule-basic))<br>
(ja-rk-rule-update)<br>
</code></pre>

<h4>SKK風ローマ字配列</h4>

<pre><code>(require "japanese.scm")<br>
(define ja-rk-rule-basic<br>
  (append '(<br>
            ((("t" "h" "a"). ())(("て" "テ" "ﾃ") ("ぁ" "ァ" "ｧ")))<br>
            ((("n" "'"). ())("ん" "ン" "ﾝ"))<br>
            ((("x" "x"). ("x"))("っ" "ッ" "ｯ"))<br>
            )<br>
          ja-rk-rule-basic))<br>
(ja-rk-rule-update)<br>
</code></pre>

<h4>T-Code風配列</h4>

<pre><code>(require "japanese.scm")<br>
(require "tcode.scm")<br>
;; ja-rk-rule-update を無効に<br>
(define ja-rk-rule-update<br>
  (lambda ()<br>
    '()))<br>
(set! ja-rk-rule tcode-rule)<br>
</code></pre>