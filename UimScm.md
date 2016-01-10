= uim-scm =

[uim:doc/UIM-SCM](http://uim.googlecode.com/svn/trunk/doc/UIM-SCM)より転載



ここではuim-scm APIの使用法と開発者向けの仕組みについて説明する。

## 概要 ##

uim-scmには二つの役割がある。

  * 入力方式の開発者にSchemeインタプリタインタフェースを提供する
  * Schemeインタプリタの実装部分を抽象化し、[LibUim](LibUim.md) の切り替え可能な基礎とする

入力方式の開発者以外はこのAPIを使わないこと。 不用意に使うと、GCによる致命的なクラッシュを引き起こすことになる。


---


The uim-scm API is responsible for following two roles.

  * Provides Scheme interpreter interfaces to input method plugin developers
  * Abstracts Scheme interpreter implementation and narrows its interfaces to provide switcheable base of libuim

Other developers should not use this API since the API easily causes fatal crash involving GC if you does not pay attention enough. Be careful.

## LispオブジェクトをGCから保護する ##

uim-scm はuim\_lispという名前のLispオブジェクト型を提供する。Lispオブジェクトは保守的なマーク・アンド・スイープGCで管理されるため、不意に回収されないよう保護しなければならない。ここでいう「保護」とは、GCに「このオブジェクトは使用中なのでマークするな」と指示することである。保護の方法は二つある。


---


uim-scm provides the lisp object type named 'uim\_lisp'. Since all of the objects are managed by a conservative mark and sweep GC, you have to protect them from undesirable collection. The word 'protection' means that instructing GC "It's in use, don't mark". There are two methods of protection.

### 静的記憶領域の保護 ###

任意の静的記憶領域をuim\_scm\_gc\_protectで割り当てることができる。この関数は、変数を使う前に呼ばなければならない。

```
static uim_lisp foo;
static uim_lisp bar;

void
uim_plugin_instance_init(void) {
  uim_scm_gc_protect(&foo);
  uim_scm_gc_protect(&bar);
}
```


---


You can allocate arbitrary static storage as for uim\_lisp by uim\_scm\_gc\_protect(). The function must be invoked before using the variables.

```
static uim_lisp foo;
static uim_lisp bar;

void
uim_plugin_instance_init(void) {
  uim_scm_gc_protect(&foo);
  uim_scm_gc_protect(&bar);
}
```

### スタックの保護 ###

スタック（自動記憶領域上）のLispオブジェクトを保護することもできる。以下の例を見てほしい。

```
char *
literalize_string(const char *str)
{
  uim_gc_gate_func_ptr func_body;
  void *ret;

  func_body = (uim_gc_gate_func_ptr)literalize_string_internal;
  ret = uim_scm_call_with_gc_ready_stack(func_body, (void *)str);

  return (char *)ret;
}

static char *
literalize_string_internal(const char *str)
{
  uim_lisp form;
  char *escaped;

  form = uim_scm_list2(uim_scm_make_symbol("string-escape"),
                       uim_scm_make_str(str));
  escaped = uim_scm_c_str(uim_scm_eval(form));

  return escaped;
}
```

uim\_lispが使われている関数では上記のように必ずuim\_scm\_call\_with\_gc\_ready\_stack()を経由して呼び出される必要がある。uim\_scm\_call\_with\_gc\_ready\_stack()はスタック領域の保護されたベースアドレスを用意する。この場合、'form'というlispオブジェクトはuim\_scm\_make\_symbol(), uim\_scm\_make\_str(), uim\_scm\_eval()の無名の返り値であり、メソッドにより保護されている（あるオブジェクトはレジスタに配置されるかもしれないが同時にレジスタは暗黙上保護される）。

関数ポインタ型であるuim\_gc\_gate\_func\_ptrはuim-scm.hで以下のように定義されている。引数と返り値は (void **)に固定されているので、複数の引数を関数に渡す必要がある場合は一時的に構造体を用意して対処する必要がある。この方法を用いている例としてuim- scm.cにあるuim\_scm\_error()がある。**

```
typedef void *(*uim_gc_gate_func_ptr)(void *);
```

「保護された」スタック領域は再帰することが可能である。つまり、uim\_scm\_call\_with\_gc\_ready\_stack()をuim\_scm\_call\_with\_gc\_ready\_stack()から呼び出された関数から呼び出すことも可能である。


---


You can also protect your lisp objects on stack (i.e. auto storage). See following example.

```
char *
literalize_string(const char *str)
{
  uim_gc_gate_func_ptr func_body;
  void *ret;

  func_body = (uim_gc_gate_func_ptr)literalize_string_internal;
  ret = uim_scm_call_with_gc_ready_stack(func_body, (void *)str);

  return (char *)ret;
}

static char *
literalize_string_internal(const char *str)
{
  uim_lisp form;
  char *escaped;

  form = uim_scm_list2(uim_scm_make_symbol("string-escape"),
                       uim_scm_make_str(str));
  escaped = uim_scm_c_str(uim_scm_eval(form));

  return escaped;
}
```

All function that uses stack-placed uim\_lisp must be called via uim\_scm\_call\_with\_gc\_ready\_stack() as above. It setups the base address of 'protected' stack region. In this case, the lisp objects 'form', anonymous return value of uim\_scm\_make\_symbol(), uim\_scm\_make\_str() and uim\_scm\_eval() are protected by the method (although some objects may be placed into registers, the registers are also protected implicitly).

The function type uim\_gc\_gate\_func\_ptr is defined as follows in uim-scm.h. Since its arguments and return type are fixed to (void **), passing multiple arguments to a function need temporary struct. See uim\_scm\_error() in uim-scm.c for example.**

```
typedef void *(*uim_gc_gate_func_ptr)(void *);
```

The 'protected' stack region can be nested. i.e. uim\_scm\_call\_with\_gc\_ready\_stack() can be invoked from a function invoked from uim\_scm\_call\_with\_gc\_ready\_stack().

## Internal ##

uim-scm API では [R5RS](http://www.schemers.org/Documents/Standards/R5RS/) の機能すべてを提供することを目的としない。 Scheme-C アダプタを書くのに本質的なものだけが追加される。 API 関数を追加したくなった場合には、それは頻繁に使うものなのか、 C で書く必要があるのかを考えてほしい。

現在の uim-scm の実装では[SigScheme](http://code.google.com/p/sigscheme/)インタプリタだけが提供されている。 名前空間汚染を避けるため、[SigScheme](http://code.google.com/p/sigscheme/)の関数と変数は公開シンボルを使って リンクするのではなく、static に定義して uim-scm.c に直接includeしてラップしている。uim-scmのAPIが洗練されてきたら、Schemeインタプリタの実装部分はuim-scm-[scheme48](http://s48.org/).cやuim-scm-[gauche](http://www.shiro.dreamhost.com/scheme/gauche/).cのようなものにも 切り換えられるようになるだろう。だが、uim/ 以下の**.[hc](hc.md)や**.scmファイルは依然として様々な点で[SIOD](http://www.cs.indiana.edu/scheme-repository/imp/siod.html)-Specific（と[SigScheme](http://code.google.com/p/sigscheme/)によるエミュレート）の特徴や振舞いに依存している。


---


The uim-scm API is not intended to provide all R5RS features. Only 'core' ones to write Scheme-C adapters should be added. Consider how frequently it will be used, and whether it should be written by C, when you want to add an API function.

Current implemenation of uim-scm only provides the [SigScheme](http://code.google.com/p/sigscheme/) interpreter. To avoid namespace pollution, all [SigScheme](http://code.google.com/p/sigscheme/) functions and variables are defined as static and wrapped into uim-scm.c by direct inclusion rather than linked via public symbols. After elaboration of uim-scm API, the Scheme interpreter implementation can be switched to another one such as uim-scm-scheme48.c or uim-scm-gauche.c. But **.[hc](hc.md) under uim/ and**.scm are still depending on SIOD-specific (and emulated by [SigScheme](http://code.google.com/p/sigscheme/)) features and behaviors in several ways.
