= uim-qt =

## これは何？ ##

uimとQtツールキットのブリッジ。 Qtのimmodule経由で入力を行う場合に使う。

このブリッジは標準では含まれません。 '''--with-qt-immodule'''もしくは'''--with-qt4-immodule'''をつけてuimをコンパイルする必要があります。

なお'''--with-qt-immodule'''はQt 3.xに[immodule for Qtパッチ](http://freedesktop.org/wiki/Software/immodule-qt)を当てたものだけをサポートしています。 このパッチが当てられていないQt 3.xで入力する場合は、[uim-xim](UimXim.md)を使用してください。

## 使い方 ##

環境変数'''QT\_IM\_MODULE'''に'''uim'''を指定する。 通常は、環境に合わせて~/.xsession、~/.xinitrc、~/.gnomerc、~/.xprofileあたりに

```
QT_IM_MODULE=uim ; export QT_IM_MODULE
```

を追記しておくだけでよいでしょう。

### 環境変数 ###

QT\_IM\_MODULE

XCOMPOSEFILE