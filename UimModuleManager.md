= uim-module-manager =

## これは何？ ##

モジュールのリストを操作するツール。 システム全体からモジュールを追加/削除する時に使います。

## 使い方 ##

適当なオプションをつけて実行します。

```
# uim-module-manager --register anthy
```

一般ユーザーで登録するには、~/.uim.d.plugin を '''--path'''オプションで指定しましょう。

```
$ uim-module-manager --register ruby --path ~/.uim.d/plugin
```

### オプション ###

--register ''モジュール名'':: モジュールを登録します。--unregister ''モジュール名'':: モジュールをUnregisterします。--unregister-all:: すべてのモジュールをUnregisterします。--path ''パス'':: installed-modules.scm、loader.scmファイルの生成先を指定します。デフォルトは''${prefix}/share/uim''です。