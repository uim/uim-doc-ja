= uim-gtk =



## これは何？ ##

uimとGTK+ツールキットのブリッジ。 GTK+のimmodule経由で入力を行う場合に使う。

## 使い方 ##

環境変数'''GTK\_IM\_MODULE'''に'''uim'''を指定する。 通常は、環境に合わせて~/.xsession、~/.xinitrc、~/.gnomerc、~/.xprofileあたりに

```
GTK_IM_MODULE=uim ; export GTK_IM_MODULE
```

を追記しておくだけでよいでしょう。

GTK+アプリケーションのテキストフォームで右クリック→「入力メソッド」→「uim」を選択する事でも使えます。 但しMozillaなど、独自のメニューを持つアプリでは、そのようなメニュー項目がない場合があります。

### 注釈検索機能 ###

EBライブラリ、ネットワーク対応辞書、カスタムフィルタによる注釈機能が使えます。
EBライブラリの場合、対応形式の辞書が必要です。

  * EB形式
  * EBG形式
  * EBXA形式
  * EBXA-C形式
  * S-EBXA形式
  * EPWING形式

JIS X 4081(EPWING互換)形式への変換プログラム、および変換済みの辞書は[FPWBOOK](http://openlab.ring.gr.jp/edict/fpw/)から入手できます。 JIS X 4081形式の辞書の場合

```
dict(任意)-+-catalogs
           `-辞書名-+-data---辞書ファイル
                    `-gaiji
```

という構造になっていますが、一番上の"dict(任意)"ディレクトリを指定する必要があります。

### ファイル ###

~/.uim.d/customs/custom-annotation.scm:: [UimPref](UimPref.md)の「注釈」ファイル。

### 環境変数 ###

GTK\_IM\_MODULE

XCOMPOSEFILE

## カスタマイズ可能な項目 ##

### EBライブラリ設定の変数 ###

| 動作 | 変数名 | 指定できる値 | デフォルト値 |
|:---|:----|:-------|:-------|
| 注釈の検索にEBライブラリを使用する | eb-enable-for-annotation? | #t #f  | #f     |
| EB辞書ファイルを収納しているディレクトリ | eb-dic-path | "文字列"  | "/usr/local/share/dict" |

#### EBライブラリの変数の依存関係 ####

  * eb-enable-for-annotation? #f
    * eb-dic-path