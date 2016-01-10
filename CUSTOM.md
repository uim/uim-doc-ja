= CUSTOM =

[uim:doc/CUSTOM](http://uim.googlecode.com/svn/trunk/doc/CUSTOM)より転載



ここではuim-custom APIの使用法と開発者向けの仕組みを説明する。

## Abstract ##

## Design basics and decisions ##

## How to define your own customs ##

## IMのコードにcustomの定義を反映させる ##

customの定義をIMに取り込むには、IMのファイルに以下のように書く。

```
(require-custom "your-custom.scm")
```

customファイルを読み込むのに普通の'require'を使わないこと。require-customはユーザごとに設定の読み込みと再読み込み管理を行うが、'require'はそういったことをしないからである。

ファイル名に「-custom」をつけるのは慣習であり、必ずしも必要ではない。しかし、ファイル管理を簡単にするためにそうすることを推奨する。


---


To acquire a defined custom in your IM, describe as following in the your IM file.

```
(require-custom "your-custom.scm")
```

Don't use ordinary 'require' to load a custom file. The require-custom performs per-user configuration loading and reload management, but ordinary 'require' does not.

"-custom" suffix of the filename is only a convention and not required. But we recommend the naming convention to manage the files easily.

## custom変数が設定されたときに手続きを呼び出す ##

custom-set-hooksという名前のhookを使うことで可能である。

```
(custom-add-hook 'anthy-input-mode-actions
                 'custom-set-hooks
                 (lambda ()
                   (puts "anthy-input-mode-actions has been set\n")
                   (anthy-configure-widgets)))
```

custom-add-hookの第3引数には引数をとらない手続きを渡す。この手続きはcustom変数anthy-input-mode-actionsが設定されたときに呼び出される。uim-helper-serverとのプロセス間通信によるcustom変数の更新でもこのフックは起動される。したがって[UimPref](UimPref.md)で変数を編集すると、それはすべてのプロセスに波及し、その場その場でフックを起動する。

例えば、以下のようなフックで[UimPref](UimPref.md)から動的ファイル切り替えが起動される。

```
(custom-add-hook 'skk-dic-file-name
                 'custom-set-hooks
                 skk-reload-dic)
```

ただし、set-hook機能にはいくつか制限がある。

  * ランタイム版のcustom機構（custom-rt.scm）はcustom変数一つにつきフックを一つしかつけられない（フル機能版では複数のフックを扱える）
  * フル機能版（custom.scm）だけで有効なcustom APIはフック手続きの中で使えない

そのようなコードは以下のように条件分岐の中に入れる。こうすることでcustom-rt.scmがフックを無視するようにする。

```
(if custom-full-featured?
    (custom-add-hook 'anthy-kana-input-method-actions
                     'custom-set-hooks
                     (lambda ()
                       (custom-choice-range-reflect-olist-val
                        'default-widget_anthy_kana_input_method
                        'anthy-kana-input-method-actions
                        anthy-kana-input-method-indication-alist))))
```


---


The feature is usable via the hook named 'custom-set-hooks'. See following example.

```
(custom-add-hook 'anthy-input-mode-actions
                 'custom-set-hooks
                 (lambda ()
                   (puts "anthy-input-mode-actions has been set\n")
                   (anthy-configure-widgets)))
```

Any procedure that takes no argument can be placed into the third argument to custom-add-hook. The procedure will be invoked when the custom variable anthy-input-mode-actions has been set. Interprocess custom variable update via uim-helper-server also triggers this hook. So some variables edited on uim-pref will be propagated to any processes and invokes the hook on the fly.

For example, dynamic file switching can be triggered by uim-pref using following hook.

```
(custom-add-hook 'skk-dic-file-name
                 'custom-set-hooks
                 skk-reload-dic)
```

There are some limitations for the set-hook feature.

  * Runtime version of the custom facility (custom-rt.scm) only accepts at most one hook per custom variable (full-featured version can handle multiple hooks)
  * Custom API enabled only in full-featured version (custom.scm) cannot be invoked in the hook procedure.

Enclose such code into conditional block as follows. This ensures that custom-rt.scm ignores the hook.

```
(if custom-full-featured?
    (custom-add-hook 'anthy-kana-input-method-actions
                     'custom-set-hooks
                     (lambda ()
                       (custom-choice-range-reflect-olist-val
                        'default-widget_anthy_kana_input_method
                        'anthy-kana-input-method-actions
                        anthy-kana-input-method-indication-alist))))
```

## custom変数のactivityを制御する ##

custom変数にはactivityという名の状態がある。これは、custom変数に設定された値が意味を成すかどうかを表す。activityは設定ツールの対応するウィジェットが編集可能かどうかということと同義であるべきである。activityをウィジェットに反映させるには、例えばgtk\_widget\_set\_sensitive()を使う。

custom変数のactivityを変更するにはフックを使う。特に指定しなければcustom変数はすべてactiveである。


---


Any custom variables has a state named 'activity'. This state indicates whether the value set in the custom variable makes sense or not. The state should be reflected to value editability of the corresponding widget on preference tools. i.e. Use gtk\_widget\_set\_sensitive() for the corresponding widget to reflect the state.

To control activity of a custom variable, configure the hook for the custom variable. Otherwise all custom variables are always active.

### Example 1: 単純なactivity ###

下の例ではmy-frequently-used-string1というcustom 変数が、ユーザー名が「yamaken」のときだけactiveになるようにしている。ここでは、custom-add-hookの第3引数はcustom変数がactiveかinactiveかを示す述語になる。

この述語が呼ばれるのは以下のときである。

  * uim\_custom\_get()でcustom変数を取得したとき
  * 明示的にcustom-active?を呼んだとき
  * custom変数が設定されたとき。詳しくは Example 2 を参照。

```
(define-custom 'my-frequently-used-string1 "I'm hungry! Give me some sweets."
  '(my-private)
  '(string)
  (_ "My frequently used string 1")
  (_ "long description will be here."))

(custom-add-hook 'my-frequently-used-string1
                 'custom-activity-hooks
                 (lambda ()
                   (string=? (getenv "USER")
                             "yamaken")))
```


---


Following example shows that the custom variable my-frequently-used-string1 is active only when username is "yamaken". The third argument of custom-add-hook can be any predicate to indicate whether the custom variable is active or inactive.

The activity is tested by the predicate when:

  * The custom variable has been acquired by uim\_custom\_get().

  * Invoking custom-active? explicitly

  * Any custom variable has been set. See next example for further information

```
(define-custom 'my-frequently-used-string1 "I'm hungry! Give me some sweets."
  '(my-private)
  '(string)
  (_ "My frequently used string 1")
  (_ "long description will be here."))

(custom-add-hook 'my-frequently-used-string1
                 'custom-activity-hooks
                 (lambda ()
                   (string=? (getenv "USER")
                             "yamaken")))
```

### Example 2: ほかのcustom変数の値を反映した動的なactivity ###

activityは他のcustom変数が設定されたときにも変化する。

ここの例ではsegment-separatorはshow-segment-separator?が真のときだけactiveになる。show-segment-separator?に新しい値が設定されると、activityは自動的に変更され、以前segment-separatorに設定したcallbackを使ってuim-customのクライアントに変更が通知される。

述語はcustom 変数が設定されたときに呼ばれる（別の値に変更される必要はない）。So you can place any flexible predicate as the third argument for the custom-add-hook.

custom変数が設定されるとactivity述語が評価され、結果はcallbackを介して通知される。

activityを決めるのに関係しあう変数を同一グループに含める必要は必ずしもない。

```
(define-custom 'show-segment-separator? #f
  '(foo)
  '(boolean)
  (_ "Show segment separator")
  (_ "long description will be here."))

(define-custom 'segment-separator "|"
  '(bar)
  '(string ".*")
  (_ "Segment separator")
  (_ "long description will be here."))

(custom-add-hook 'segment-separator
                 'custom-activity-hooks
                 (lambda ()
                   show-segment-separator?))
```


---


The activity alters when other custom variables have been set.

In following example, segment-separator will be active only when show-segment-separator? is true. The activity will be changed automatically and noticed to client of uim-custom via callback for the segment-separator previously set immediately after new value of show-segment-separator? has been set.

The predicate will be evaluated when any of custom variables have been set (changing to different value is not required). So you can place any flexible predicate as the third argument for the custom-add-hook.

All activity predicates will be evaluated and noticed via corresponding callback when any of custom variables has been set.

No group relationships including subgrouping is not required to set variable relationships.

```
(define-custom 'show-segment-separator? #f
  '(foo)
  '(boolean)
  (_ "Show segment separator")
  (_ "long description will be here."))

(define-custom 'segment-separator "|"
  '(bar)
  '(string ".*")
  (_ "Segment separator")
  (_ "long description will be here."))

(custom-add-hook 'segment-separator
                 'custom-activity-hooks
                 (lambda ()
                   show-segment-separator?))
```
