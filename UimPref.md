= uim-pref =

## これは何？ ##

![http://pdx.freedesktop.org/~kzk/uim/uim-prefs.png](http://pdx.freedesktop.org/~kzk/uim/uim-prefs.png)

uimのカスタマイズツール。 uim-pref-gtk、uim-pref-qtとuim-pref-qt4が用意されています。

なおuim-pref-qtとuim-pref-qt4は標準では含まれません。uim-pref-qtは'''--with-qt'''、uim-pref-qt4は'''--with-qt4'''をつけてuimをコンパイルする必要があります。

## 使い方 ##

ターミナルエミュレータなどからuim-pref-gtkもしくはuim-pref-qtを起動して使います。

```
$ uim-pref-gtk &
```

また[UimToolbar](UimToolbar.md)から起動する事もできます。

## より高度なカスタマイズ ##

uim-prefで提供されているカスタマイズの項目以上のカスタマイズをするには、自分でSchemeコードを書く必要があります。 詳しくは[CustomizeUim](CustomizeUim.md)のページを参照してください。

## 既知のバグ ##

### 全体キー設定が各入力方式のキー設定に反映されない ###

uim-prefがuim-custom APIを完全にサポートしていないためです。

[http://garakuta.homelinux.org/~nosuke/diary/diary.html?y=2006&m=7&d=12&n=1#12-1](http://garakuta.homelinux.org/~nosuke/diary/diary.html?y=2006&m=7&d=12&n=1#12-1)
