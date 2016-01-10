= uim.el =



## これは何？ ##

![http://garakuta.homelinux.org/~nosuke/tsubo/files/linux/uim_el.png](http://garakuta.homelinux.org/~nosuke/tsubo/files/linux/uim_el.png)

uim.elは、uimとEmacsの間を結ぶブリッジです。

Emacs上から、uimのサポートしている入力方式を直接利用できるようになります。

## 特徴 ##

uim.elは、uimとEmacsの間を結ぶブリッジです。

uim.elを導入することで、様々なインプットメソッドをuimを通じてEmacs上で利用することが可能になります。

### 対応するEmacs ###

  * GNU Emacs 20系以上
    * 20.7.1，21.4.1, 22.1.1 で動作確認
  * XEmacs 21系
    * 21.4.20 (sumo + mule-sumo) で動作確認

これ以前のもの（Mule-2.3 や Emacs-19.x など）には対応しません。 GNU Emacs 23系（CVS版）では動作するかもしれません。

## クイックスタート ##

uim.elは、Emacsのマイナーモード（uim-mode）として実装されています。

Emacsでuim.elを使う方法には、uim-modeを直接呼び出して利用する方法と、LEIMを介して利用する方法の、2通りがあります。

いずれの場合も、.emacs）あるいは他のEmacsの設定のためのファイル）にいくつか記述を加える必要があります。また、どちらを選んでもuim.elの提供する機能に変わりはありません。

もし、あなたがuim.elの提供するIMと、それ以外のEmacs上のIMを頻繁に切り換えて利用するのであれば、LEIMを利用した方がよいでしょう。

### uim-modeを直接呼び出して利用する場合の設定 ###

```
;; uim.elを読み込む
(require 'uim)
;; Emacs起動時に読み込んでほしくない場合は、上記をコメントアウトし、
;; 代わりに下記の行をアンコメント
;;(autoload 'uim-mode "uim" nil t)

;; uim-modeをトグルするためのキーバインド（C-oを使う場合の例）
(global-set-key "\C-o" 'uim-mode)
```

まずrequire関数でuim.elを直接ロードします。

```
(require 'uim)
```

あるいは、必要なときになって初めてuim.elを読み込むようにしたいので あれば、require関数の代わりにautoload関数を使います。

```
(autoload 'uim-mode "uim" nil t)
```

次に、uim-modeをトグルするために、uim-modeコマンドのキーバインドを定義します。例えば、uim-modeのトグルにC-oを使うのであれば、以下を記述します。

```
(global-set-key "\C-o" 'uim-mode)
```

### LEIMを介して利用する場合の設定 ###

```
;; uim.elを読み込みEmacsへIMを登録する
(require 'uim-leim)

;; デフォルトのIMをuim提供のものに設定 (以下はAnthyの例)
(setq default-input-method "japanese-anthy-uim")
```

まず、require関数でuim-leim.elをロードします。ここでuimの提供するIMがEmacsに登録され、LEIMで利用可能になります。

```
(require 'uim-leim)
```

LEIMを利用した場合、uimの提供するIMは、LEIMの形式の名前でEmacsに登録されます。LEIMの形式の命名規則は以下の通りです。

```
"<Emacsでの言語名>-<uimの返してくるIM名>-uim"
```

例えば、uim-anthyであれば、uimの返してくるIM名は"anthy"で、日本語を示すEmacsの言語名は"japanese"なので、LEIMに登録される名称は"japanese-anthy-uim"となります。

uim.elの提供するものも含めて、LEIMで利用可能なIMの一覧は、以下のコマンドで確認することができます。

```
M-x list-input-method
```

LEIMのデフォルトのIMは、default-input-method変数にIM名を設定することで指定できます。もしuim-anthyをLEIMのデフォルトのIMとしたければ、以下のように記述します。

```
(setq default-input-method "japanese-anthy-uim")
```

## 普通のカスタマイズ ##

### uim-modeのデフォルトのIMをuim全体と独立に設定する ###

デフォルトでは、uim-modeが有効になると、uim-pref-gtkなどのツールで設定されたIMが有効になります．

もし、uim全体の設定とは異なるIMをデフォルトで利用したければ、uim-default-im-engine変数にそのIM名を設定して下さい。例えばuim-anthyをデフォルトで利用したければ、以下を記述します。

```
(setq uim-default-im-engine "anthy")
```

### インライン変換候補表示機能をデフォルトで有効にする ###

uim.elは、変換候補を入力中の文字列のすぐ下（もしくはすぐ上）に縦方向に並べて表示する機能を備えています。uim.elではこれを「インライン変換候補表示機能」と呼んでいます。

インライン変換候補表示機能はuim.elの最も重要な特徴の一つなのですが、プロポーショナルフォントを利用している場合、表示が崩れてしまうため。デフォルトでは無効化されています。

もしあなたがEmacsで等幅フォントを利用しているのであれば、インライン変換候補表示機能を有効にすることをお勧めします。

インライン変換候補表示機能をデフォルトで有効にしたい場合は、以下の例のようにuim-candidate-display-inline変数にnil以外の値を設定します。

```
(setq uim-candidate-display-inline t)
```

特定のメジャーモードにおいてのみ、インライン変換候補表示機能を有効（もしくは無効）にしたい場合は、uim-candidate-display-inline変数をバッファローカルにした上で、非nil（もしくはnil）をセットして下さい。

例えば、インライン変換候補表示機能をtext-modeでのみ有効にするには、以下のように記述します。

```
(setq uim-candidate-display-inline nil)

(add-hook 'text-mode-hook
          (lambda ()
	    (make-variable-buffer-local 'uim-candidate-display-inline)
            (setq uim-candidate-display-inline t)))
```

### プリエディット文字列や変換候補の色を変更する ###

uim.elは、プリエディット文字列や変換候補の装飾に以下のフェイスを用いています。

```
- uim-preedit-highlight-face  : プリエディット文字列のハイライト部分
- uim-separator-face          : プリエディット文字列の区切り文字
- uim-candidate-odd-face      : 奇数番目の変換候補
- uim-candidate-even-face     : 偶数番目の変換候補
- uim-candidate-selected-face : 選択中の変換候補
- uim-candidate-nth-face      : 選択中の変換候補の番号
```

これらの色を変更したい場合、.emacsなどに以下のように記述します。

```
(set-face-foreground 'uim-preedit-highlight-face "white")
(set-face-background 'uim-preedit-highlight-face "blue")
(set-face-foreground 'uim-separator-face "white")
(set-face-foreground 'uim-candidate-odd-face "blue")
(set-face-background 'uim-candidate-odd-face "white")
(set-face-foreground 'uim-candidate-even-face "blue")
(set-face-background 'uim-candidate-even-face "yellow")
(set-face-foreground 'uim-candidate-selected-face "blue")
(set-face-background 'uim-candidate-selected-face "white")
(set-face-foreground 'uim-candidate-nth-face "red")
(set-face-background 'uim-candidate-nth-face "white")
```

なお、Emacsで利用可能な色とその名称は、以下のコマンドで確認することができます。

```
M-x list-colors-display
```

uim.elをautoloadで読み込む設定にしている場合，以下のように、上記の設定をuim-load-hookの中に記述してください。

```
(add-hook 'uim-load-hook
           '(lambda ()
             (set-face-foreground 'uim-preedit-highlight-face "white")
             (set-face-background 'uim-preedit-highlight-face "blue")

               ...

             (set-face-background 'uim-candidate-nth-face "white")
             ))
```

### プリエディットや変換候補に枠を付ける ###

uim.elは、プリエディットや変換候補の境界をASCII文字で描画する機能を備えています．

Emacsやターミナルエミュレータが下線や色のついた文字の表示に対応していない場合に備え、uim.elでは

プリエディットの両脇にフェンスを表示させるには、以下を記述します。

```
(setq-default uim-preedit-display-fences t)
```

変換候補のフレームを表示するには、以下を記述します。

```
(setq-default uim-candidate-display-frame t)
```

### 特定のメジャーモードにおいてuim.elを最初から有効にする ###

特定のメジャーモードにおいてuim.elを最初から有効にするには、メジャーモードのフックの中でuim-mode関数を、1以上の数を引数に呼びます。

uim-modeを直接利用している場合は以下のように記述します。

```
(add-hook 'html-mode-hook
          '(lambda () (uim-mode 1)))
```

LEIMを利用している場合は、以下のように記述します。

```
(add-hook 'html-mode-hook
          '(lambda () (toggle-input-method)))
```

## 特殊なカスタマイズ ##

### 各IMの標準の入力モードを変更する ###

各IMの標準の入力モード（「ひらがな入力」や「半角カタカナ入力」など）を、uimの全体設定とは異なる値に変更したい場合は、設定を列挙したリストをuim-default-im-propに設定します。

たとえば、uim-anthyとuim-skkに関して、uim.elが起動すると同時にひらがな入力モードにしておきたい場合は、以下のように.emacsに記述します。

```
(setq uim-default-im-prop
      '("action_anthy_hiragana" "action_skk_hiragana"))
```

なお、"action\_anthy\_hiragana"などの値に関しては、まとまったドキュメントが存在しないため、各種モードの値を得るには、uimのScheme記述必要があります。

以下のようにSchemeファイルをgrepすると見つかるかもしれませんが、あまり良い方法ではありません。

```
$ grep -r register-action /usr/share/uim/*.scm
```

### ターミナルモードでのEscapeキーの挙動を変更する ###

Emacsを -nwオプションをつけてターミナル上で起動した場合、uim.elはファンクションキーや矢印キーなどの特殊なキーを認識するために、デフォルトでは単独で押下されたEscapeをuim側に渡さないようになっています。そのため，uim側で単独のEscapeにバインドされた処理をEmacs上で呼び出す場合、Escapeを2回続けて入力しなければなりません。

これがどうしても嫌な場合は、uim-use-single-escape-on-terminal変数を非nilにすることで、プリエディット文字列表示中に単独のEscapeを有効にすることができます。

```
(setq uim-use-single-escape-on-terminal t)
```

この設定を行うと、ファンクションキーや矢印キーなどの特殊なキーの他、Altキーを組み合わせたキーバインドなども正しく動作しなくなるため、お勧めしません。

## コマンド ##

uim-mode:: uim-modeを直接利用している場合に，uim.elのオンオフを切り替えます．uim-im-switch:: uim.elをマイナーモードで直接利用している場合に、現在のバッファで利用しているIMを変更します。入力後、Tabを押すと、利用可能なIMが一覧表示され、選択できます（LEIMでuim.elを利用している場合は、set-input-methodコマンドを利用してIMを切り替えて下さい）。uim-switch-candidate-display-mode:: 現在のバッファのインライン変換候補表示機能のオンオフを切り替えます。uim-reorder-minor-mode-map-alist:: マイナーモードのキーマップを並び替えて、uim.elのマップを先頭に移動させます。詳細はFAQを参照してください。uim-el-version:: uim.elのバージョンを表示します。

## FAQ ##

### Q. gtags-modeを起動すると、[UimAnthy](UimAnthy.md)をオンにできなくなります。私は、[UimAnthy](UimAnthy.md)のオン/オフにAlt+Spaceを割り当てています。 ###

A. Emacsをターミナル上で起動しており、内部でEscapeで始まるキーマップを備えたマイナーモード（gtags-modeなど）をuim.elより後に読み込んでしまうと、このような問題が発生します。

このような問題は、他のマイナーモードを有効にした後に、マイナーモードのキーマップ列を並び替え、先頭にuim.elのキーマップを移動させることで解消可能です。

uim-reorder-minor-mode-alist関数が、その機能を提供します。

たとえば、.emacsで以下のようにしてgtags-modeを起動しているなら。

```
(add-hook 'c-mode-common-hook
          '(lambda ()
            (gtags-mode 1)))
```

次のように、gtags-modeを起動した後でuim-reorder-minor-mode-alistを呼び出すようにします。

```
(add-hook 'c-mode-common-hook
           '(lambda ()
             (gtags-mode 1)
             (uim-reorder-minor-mode-map-alist)))
```

### Q. LaTeXファイルを編集していると、uim.elが変換候補を出したり消したりするたびに、行がピクピク動くことがあります。一体何が起きているのですか？ ###

A. これは、Emacs-22.xのlatex-modeが、「^」や「_」の後の文字のフォントサイズを小さくしてしまうというお節介な仕様が原因です。_

気になるのであれば、以下の設定を.emacsに追加して、latex-modeで上付き文字や下付き文字の部分のサイズが小さくならないようにして下さい。

```
(add-hook 'latex-mode-hook
          '(lambda ()
             (setq tex-verbatim-face nil)
             (defun tex-font-lock-suscript () nil)))
```

### Q. インライン変換候補表示が突然無効化されてしまうことがあります。なぜですか？ ###

A. おそらく、uim.elが変換候補を表示しようとしている領域にオーバレイが存在していると思われます。

uim.elは、技術的な理由から、オーバレイのある領域に変換候補を表示することができません。変換候補が表示されるべき領域にオーバレイが存在した場合、インライン変換候補表示機能は一時的に無効化されます。

例えば、flyspell-modeやshow-paren-mode，mmm-modeなどがオーバレイを利用しています。また、Mewのヘッダ入力欄でも利用されています。これらモードとuim.elを一緒に利用した場合、インライン変換候補表示が無効化される場合があります。

### Q. Emacsでプロポーショナルフォントを利用している場合に、変換候補の表示が崩れます。どうすれば直りますか？ ###

A. 残念ながら、プロポーショナルフォントを利用している限り、インライン変化候補の表示の崩れを防ぐことはできません。

どうしてもプロポーショナルフォントを利用したいのであれば、インライン変換候補表示を無効化するか、さもなくは崩れるのを我慢して下さい。

### Q. uim.elを有効にしていると、私のよく使うキー操作が正常に機能しませんがなぜですか？ ###

A. uim.elは、ありとあらゆるキー操作を横取りして一度uimに渡すことをしています．そのため、元々の特殊な方法で実装されている一部のキー操作は、uim.elを有効にした場合、正常に利用できなくなってしまう可能性があります。

そのようなキー操作は、見付け次第uim.elを改良して対応するようにしていますが，作者が一度も使ったことのないキー操作の中には、正常に動作しないものが含まれているかもしれません。

もし、uim.elをONにすると利用できなくなってしまうキー操作を見つけたら、是非[Bugzilla](https://bugs.freedesktop.org/)や[MailingList](MailingList.md)で報告してください。

### Q. **-modeをuim.elと組み合わせて利用すると奇妙な振る舞いを示すのですがなぜですか？ ###**

A. 前述のuim.elの特殊性から、uim.elを特定のモードと組み合わせて利用した場合に、そのモードがおかしな挙動を示す可能性は十分考えられます。

もし、そのようなモードを見つけたら、是非[Bugzilla](https://bugs.freedesktop.org/)や[MailingList](MailingList.md)で報告してください。

### Q. 時々、突然Emacsが操作不能になります。しばらくすると復活するのですが、uim-modeが無効化されてしまいます。 ###

A. おそらく、uim.elのバックエンドプログラム（uim-el-agentもしくはuim-el-helper-agent）がクラッシュしたと思われます。

再現性があるようでしたら、是非[Bugzilla](https://bugs.freedesktop.org/)や[MailingList](MailingList.md)で報告してください．

### Q. 私は[UimAnthy](UimAnthy.md)を使っています。Emacsをターミナルエミュレータ上で起動した場合、Shift+→およびShift+←で文節の伸ばし縮みができません．なぜでしょうか？ ###

A. おそらく、以下の3つの理由のどれかによるものでしょう。

  1. Shift+←/→がウィンドウマネージャやターミナルエミュレータ自身のショートカットとして定義されている
  1. ターミナルエミュレータがShift+矢印キーを認識・処理できない
  1. ターミナルエミュレータが渡してくるShift+矢印キーのエスケープシーケンスをEmacsが理解できていない

1は単純です。ウィンドウマネージャや、ターミナルエミュレータの設定を修正し、この有害なショートカットを無効化して下さい。

2は深刻です。シフト＋矢印キーの利用を諦めるか、あるいは他のターミナルエミュレータに乗り換えるしかありません。

3は、.emacsにエスケープシーケンスと対応するキーのペアを追加することで修正可能です。

例えば、GNU Emacsは、以下を設定に加えることで、おそらくは大概のターミナルエミュレータに対応できます。

```
;; xterm，mltermなど
(define-key function-key-map [27 79 49 59 50 65] [S-up])
(define-key function-key-map [27 79 49 59 50 66] [S-down])
(define-key function-key-map [27 79 49 59 50 67] [S-right])
(define-key function-key-map [27 79 49 59 50 68] [S-left])

(define-key function-key-map [27 79 49 59 53 65] [C-up])
(define-key function-key-map [27 79 49 59 53 66] [C-down])
(define-key function-key-map [27 79 49 59 53 67] [C-right])
(define-key function-key-map [27 79 49 59 53 68] [C-left])

(define-key function-key-map [27 79 49 59 54 65] [C-S-up])
(define-key function-key-map [27 79 49 59 54 66] [C-S-down])
(define-key function-key-map [27 79 49 59 54 67] [C-S-right])
(define-key function-key-map [27 79 49 59 54 68] [C-S-left])

;; mrxvtなど
(define-key function-key-map [27 91 49 59 50 65] [S-up])
(define-key function-key-map [27 91 49 59 50 66] [S-down])
(define-key function-key-map [27 91 49 59 50 67] [S-right])
(define-key function-key-map [27 91 49 59 50 68] [S-left])

(define-key function-key-map [27 91 49 59 53 65] [C-up])
(define-key function-key-map [27 91 49 59 53 66] [C-down])
(define-key function-key-map [27 91 49 59 53 67] [C-right])
(define-key function-key-map [27 91 49 59 53 68] [C-left])

(define-key function-key-map [27 91 49 59 54 65] [C-S-up])
(define-key function-key-map [27 91 49 59 54 66] [C-S-down])
(define-key function-key-map [27 91 49 59 54 67] [C-S-right])
(define-key function-key-map [27 91 49 59 54 68] [C-S-left])

;; urxvt など
(define-key function-key-map [27 91 97] [S-up])
(define-key function-key-map [27 91 98] [S-down])
(define-key function-key-map [27 91 99] [S-right])
(define-key function-key-map [27 91 100] [S-left])

(define-key function-key-map [27 79 97] [C-up])
(define-key function-key-map [27 79 98] [C-down])
(define-key function-key-map [27 79 99] [C-right])
(define-key function-key-map [27 79 100] [C-left])
```

### Q. かな入力時に、「ろ」と「ー」のどちらのキーを押しても「ろ」が入力されてしまいます。どうすれば「ー」のキーで「ー」が入力されるようになりますか？ ###

A. 残念ながら、これを実現する良い方法を私たちは知りません。

少なくともGNU Emacs上で動作しているELISPのプログラムから、これら2つのキーのどちらが押されたかを区別することができません。GNU Emacsは、単に「\」（バックスラッシュ）キーが押されたとしか認識しないのです。

### Q. 今朝CVSからチェックアウトしてきたEmacsだとuim.elが動きません！早く何とかしてください！ ###

A. ごめんなさい。CVSの最先端のバージョンは、しばしばおかしなバグが混入するため、現在は積極的なサポートをしていません。

### "C-h (Type ? for further options)-" ###

上記のメッセージが出る場合は、~/.emacsに

```
(uim-reset-keymap)
```

を追加してください。

http://garakuta.homelinux.org/~nosuke/diary/200601.html#4-2

### vi協調モードをオンにしているとESCを押したときに直接入力に戻ってしまう ###

  * [http://garakuta.homelinux.org/~nosuke/diary/diary.html?y=2008&m=5&d=15&n=1#15-1](http://garakuta.homelinux.org/~nosuke/diary/diary.html?y=2008&m=5&d=15&n=1#15-1)
  * [http://garakuta.homelinux.org/~nosuke/diary/diary.html?y=2009&m=1&d=2&n=1#2-1](http://garakuta.homelinux.org/~nosuke/diary/diary.html?y=2009&m=1&d=2&n=1#2-1)

~/.emacsに以下を追記。

```
(defadvice uim-change-im (around uim-custom-change-im activate)
  (progn
    ad-do-it
    (uim-do-send-recv-cmd
     ;; uim-anthyの場合
     (format "%d HELPER prop_update_custom anthy-use-with-vi? #f"
        uim-context-id))))
```
