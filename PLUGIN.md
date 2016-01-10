= PLUGIN =

[uim:doc/PLUGIN](http://uim.googlecode.com/svn/trunk/doc/PLUGIN)より転載



Plugin for uim


## 伝統的な方式 ##

uim では入力システムのモジュール化のため、
共有ライブラリと Scheme プログラムをロードする
プラグインシステムが実装されている。

uimのプラグインはSchemeとライブラリのどちらか、あるいは両方から構成される。

```
    ___________    (require-module "foo")
   |           | ------------------+--->  libuim-foo.so
   |  libuim   |                   |
   |___________|                   +--->  foo.scm
```


---

uim supports plugin system which loads dynamic library and scheme definition
as a input method module.

uim's plugin may consist of scheme file and/or dynamic library.

Schemeエンジンから
(require-module "foo")が呼び出されると、libuim-foo.soがメモリに
ロードされると同時に'uim\_dynlib\_instance\_init'を実行する。
libuim-foo.soの呼び出しの後、'foo.scm'がロードされる。

---

When called (require-module "foo") from libuim scheme engine, libuim-foo.so
is loaded if existed and call 'uim\_dynlib\_instance\_init' in libuim-foo.so first.
After that 'foo.scm' is loaded if existed.

### ユーザが使用する場合 ###

サードパーティのプラグインをインストールしたい場合、
共有ライブラリファイルと Scheme ファイルを ~/uim.d/plugin/
に置く必要がある。例えば、"foo"というプラグインをインストールする場合
、~/uim.d/plugin/ にlibuim-foo.soと foo.scm を置かなければならない。
その後、以下のコマンドを実行し、uim-pref でそのプラグインを有効にする
必要がある。。

```
   $ uim-module-manager --register foo --path=~/.uim.d/plugin
```

---

If you want to install 3rd party plugin, you have to place both the dynamic
shared object and scheme file to ~/.uim.d/plugin/.
For example, if you want to install "foo", you have to put both
libuim-foo.so and foo.scm to ~/.uim.d/plugin. And you need to invoke
following command to enable the plugin.


### 管理者が全ユーザに使用させたい場合 ###

サードパーティのプラグインをインストールする場合は、
共有ライブラリファイルを${pkglibdir}/plugin/に置き、
Scheme ファイルを ${pkgdatadir}/plugin に置く必要がある。
例えば、"foo"というプラグインをインストールする場合には
libuim-foo.soを${pkglibdir}/pluginに、foo.scm を ${pkgdatadir}/plugin
に置かなければならない。さらに、このプラグインを全ユーザに対して
有効にする場合には、以下のコマンドを実行する必要がある。
```
$ sudo uim-module-manager --register foo
```

---

If you want to install 3rd party plugin, you have to place the dynamic shared
object to ${pkglibdir}/plugin/ and place the scheme library to ${pkgdatadir}/.

For example, if you want to install "foo", you have to install libuim-foo.so
to ${pkglibdir}/plugin and foo.scm to ${pkgdatadir}/. If you want to enable
this for all users, invoke following command.


### プラグイン開発をする場合 ###

  * uim\_dynlib\_instance\_init(void): Called when plugin is being loaded. In most case, initialize variables and bind scheme symbol and C functions.

  * uim\_dynlib\_instance\_quit(void): Called when plugin is being unloaded.

Plugin's loading scheme

1. Plugin loading: dlopen(libuim-foo.so) -> call uim\_dynlib\_instance\_init -> call "foo.scm"

2. Plugin unloading: call uim\_dynlib\_instance\_quit -> dlclose(libuim-foo.so)


## Dynamic library loading ##

From 1.6.0, uim supports plugin system which loads dynamic library explicitly
from scheme file.  Use this system if you want to use external C code or
library from scheme side.

```
    ___________  (require "foo") --> (require-dynlib "bar")
   |           |
   |  libuim   | ---------->  foo.scm --------> libuim-bar.so
   |___________|
```

When called (require-dynlib "bar") from the top of foo.scm, libuim-bar.so is
loaded and 'uim\_dynlib\_instance\_init' in libuim-bar.so is called.

### For developers ###

  * uim\_dynlib\_instance\_init(void): Called when plugin is being loaded. In most case, initialize variables and bind scheme symbol and C functions.

  * uim\_dynlib\_instance\_quit(void): Called when plugin is being unloaded.

Plugin's loading scheme:

1. Plugin loading: (require-dynlib "foo") -> dlopen(libuim-foo.so) -> call uim\_dynlib\_instance\_init -> (provide "foo")

2. Plugin unloading: (dynlib-unload "foo") -> call uim\_dynlib\_instance\_quit -> dlclose(libuim-foo.so)