= コーディングスタイル =

[A coding style proposal for uim (was Re: コミットポリシーに関して)](http://lists.sourceforge.jp/pipermail/anthy-dev/2005-October/002506.html)より転載

```
/* derived from: http://cvsweb.netbsd.org/bsdweb.cgi/src/share/misc/style?rev=HEAD&content-type=text/x-cvsweb-markup */

/*
 * Macros are capitalized.
 * If they are an inline expansion of a function, the function is defined
 * all in lowercase, the macro has the same name all in uppercase.
 * If the macro is an expression, wrap the expression in parenthesis.
 * If the macro is more than a single statement, use ``do { ... } while (0)'',
 * so that a trailing semicolon works.
 * Right-justify the backslashes to column 78; it makes it easier to
 * read. The CONSTCOND comment is to satisfy lint(1).
 */
#define MACRO(v, w, x, y)                                                    \
  do {                                                                       \
    v = (x) + (y);                                                           \
    w = (y) + 2;                                                             \
  } while (/* CONSTCOND */ 0)

#define DOUBLE(x) ((x) * 2)

/* Enum types are capitalized.  No comma on the last element. */
enum EnumType {
  ONE,
  TWO
} et;

/* Do inline return type and function name of a function prototype. */
int uim_init(void);

/* If the line overflows column 79, fold it at a comma. */
uim_candidate uim_get_candidate(uim_context uc, int index,
                                int accel_enumeration_hint);

/* If the line overflows column 79 even if folded, leave it untouched. */
void uim_set_prop_label_example(uim_context uc, int a_very_long_long_long_long_long_long_long_long_name);

/*
 * But if the parameter is a function pointer with direct type definition,
 * fold it into dedicated line.
 *
 * DO NOT declare a pointer in C++-style
 * E.g. use "void *ptr", not "void* ptr"
 */
void uim_set_prop_label_update_cb(uim_context uc,
                                  void (*update_cb)(void *ptr, const char *str));

/*
 * A function pointer with direct type definition must always be written
 * in single line even if its parameter can be folded.
 */
void uim_set_preedit_cb(uim_context uc,
                        void (*clear_cb)(void *ptr),
                        void (*pushback_cb)(void *ptr, int attr, const char *str),
                        void (*update_cb)(void *ptr));

/*
 * DO NOT declare a pointer in the C++-style such as "char* p".
 *
 * Even if the "char*" style notation does not cause compile error, such
 * coding style is a bad habit that leads a human error from
 * misinterpretation on a type declaration.
 *
 * For example, a declaration "char* a, b, c;" may sometimes be
 * interpreted as "char* a; char* b; char* c;" by less-experienced C/C++
 * programmers. But it of course results "char* a; char b; char c;". The
 * notation imitating 'ideal' type definition such as "'cp' is a 'char*'"
 * is a poisonous syntax sugar. To keep original semantic interpretation
 * over a type of C, do not use it. "char *cp" should be readable as
 * "applying '*' operator to the 'cp' makes char".
 *
 * So we should write pointers as "char *" style. "char *a, b, c;" will
 * not cause such misinterpretation. We should remind that the uim library
 * will be used by wide-range of programmers. We should make efforts for
 * eliminating sources of human errors.
 */
static const void *vp;            /* Not "void* vp;" */
static const char *cp, **cps, c;  /* Not "char* cp," */

/*
 * The function type must be declared on a line by itself
 * preceding the function.
 */
static const char *
select(int argc, char *argv[])
{
  /*
   * Separate variable declaration block and subsequent codes by a blank
   * line, and DO NOT initialize variables in the declarations. This makes
   * an abstract about what this function does, in combination with the
   * function name, at a glance.
   *
   * DO NOT declare a pointer in C++-style such as "char* p".
   * DO NOT declare a variable in a middle of block as C++/C99-style.
   */
  int score, best_score;
  int (*evaluate)(const char *);
  const char *cp, *selected, *candidate, **candidates;

  // DO NOT USE C++/C99-STYLE COMMENT!

  /* No spaces after function names. */
  if ((result = function(a1, a2, a3, a4)) == NULL)
    exit(1);

  /* Unary operators don't require spaces, BINARY OPERATORS DO. */
  a = ((b->c[0] + ~d == (e || f)) || (g && h)) ? i : (j >> 1);
  k = !(l & FLAGS);

  /*
   * DO SPACE AFTER KEYWORDS (while, for, return, switch).  No braces are
   * used for control statements with zero or only a single statement,
   * unless it's a long statement.
   *
   * Forever loops are done with for's, not while's.
   */
  for (p = buf; *p != '\0'; ++p)
    continue;  /* Explicit no-op */
  for (;;)
    stmt;

  /*
   * Use `!' for tests even if it's not a boolean.
   * E.g. use "if (!*p)", not "if (*p == '\0')".
   *      use "if (!p)",  not "if (p == NULL)".
   *
   * Developers should aware of type of the variable without such explicit
   * type-specific comparison.
   *
   * The heart of the C language is that all primitive types define zero
   * as the false value, and it can directly be a boolean conition. Making
   * it obsolete is an excessive anti-incorrectness movement of C++-ism, I
   * think.
   */
  best_score = 0;
  for (candidate = *candidates; candidate; candidates++) {
    score = 0;
    for (cp = candidate; *cp; cp++) {
      if (*cp == ' ')
        score = -1;
    }
    /*
     * An inequality expression should always be written as
     * (lesser < greater) order regardless of which side is the
     * subject. It helps visualizing the numeric positions as a number
     * line in an intuitive interpretation, especially in a range
     * comparison as follows.
     *
     * Ruby: (worst..best) === n
     * C:    (worst <= n && n <= best)
     */
    if (0 <= score)
      score = (*evaluate)(candidate);
    if (best_score <= score)
      selected = candidate;
  }

  /*
   * Casts and sizeof's are not followed by a space.
   *
   * Use `!' for tests even if it's not a boolean.
   * E.g. use "if (!*p)", not "if (*p == '\0')".
   *      use "if (!p)",  not "if (p == NULL)".
   *
   * DO NOT cast a pointer in C++-style.
   * E.g. use "(int *)p", not "(int*)p"
   *
   * Do not use C++ style '0' for a NULL pointer.
   * Routines returning ``void *'' should not have their return
   * values cast to more specific pointer types.
   *
   * Use uim_err/uim_warn (may be added), don't roll your own!
   */
  if (!(four = malloc(sizeof(struct foo))))
    uim_err(1, NULL);
  if (!(six = (int *)overflow()))
    uim_err(1, "Number overflowed.");
  while (*strp++)
    continue;

  /*
   * Closing and opening braces go on the same line as the else.
   * Don't add braces that aren't necessary except in cases where
   * there are ambiguity or readability issues. But if a body
   * statement of if-else sequence has braces, all other parts must
   * also have even if single statement.
   */
  if (test) {
    /*
     * I have a long comment here.
     */
#ifdef zorro
    z = 1;
#else
    b = 3;
#endif
  } else if (bar) {
    stmt;
    stmt;
  } else {  /* Add braces even if single statement */
    stmt;
  }
  /* single statement does not need braces */
  if (test)
    stmt;
  else if (bar)
    stmt;
  else
    stmt;

  /*
   * Elements in a switch statement that cascade should have a FALLTHROUGH
   * comment.  Code that cannot be reached should have a NOTREACHED comment.
   */
  while ((ch = getopt(argc, argv, "abn")) != -1) {
    switch (ch) {           /* Indent the switch. */
    case 'a':               /* Don't indent the case. */
      aflag = 1;
      /* FALLTHROUGH */
    case 'b':
      bflag = 1;
      break;
    case 'n':
      errno = 0;
      num = strtol(optarg, &ep, 10);
      break;
    case '?':
    default:
      usage();
      /* NOTREACHED */
    }
  }

  /*
   * Parts of a for loop may be left empty.  Don't put declarations
   * inside blocks unless the routine is unusually complicated.
   */
  for (; cnt < 15; cnt++) {
    stmt1;
    stmt2;
  }

  /* Second level indents are also two spaces. */
  while (cnt < 20)
    z = a + really + long + statement + that + needs + two lines +
      gets + indented + four + spaces + on + the + second +
      and + subsequent + lines;

  /*
   * a return statement at end of a function should be separated by a
   * blank line.
   * No parentheses are needed around the return value.
   */
  return selected;
}
```

http://lists.sourceforge.jp/mailman/archives/anthy-dev/2005-October/002580.html

```
> /* Enum types are capitalized.  No comma on the last element. */
> enum EnumType {
>   ONE,
>   TWO
> } et;

型名を capitalize するのは統一性に欠ける。列挙型であることを明示したいな
ら typedef しなければいい。
enum enum_type {
  ONE,
  TWO
} et;
とするべき。

>   /*
>    * Separate variable declaration block and subsequent codes by a blank
>    * line, and DO NOT initialize variables in the declarations. This makes
>    * an abstract about what this function does, in combination with the
>    * function name, at a glance.

大賛成。

>   /*
>    * Use `!' for tests even if it's not a boolean.
>    * E.g. use "if (!*p)", not "if (*p == '\0')".
>    *      use "if (!p)",  not "if (p == NULL)".
>    *
>    * Developers should aware of type of the variable without such explicit
>    * type-specific comparison.
>    *
>    * The heart of the C language is that all primitive types define zero
>    * as the false value, and it can directly be a boolean conition. Making
>    * it obsolete is an excessive anti-incorrectness movement of C++-ism, I
>    * think.
>    */

ダウト。数値の大小比較の special case に 0 が登場するときは == 0 とした
方が意味的にも、視覚的にも正確。例: strcmp(), memcmp()

それからヤマケンさんが挙げている例は、いずれも「0 である場合」「0 でない
場合」の二つで大きな隔たりがあるけど、「0 以外のどれであるか」によって定
性的な差は出ない。そういう意味で if(*p) / if (p) は boolean test です。
この場合は私はどっちでもいい。むしろ if (p) でサボりたいときもあれば、
for (p = a[0]; p != NULL; p++) みたいに条件を目立たせたいときもある。
どっちで書かなくてはいけない、というのを決める意義は無いと思う。

ただしはっきりと boolean test なものは比較無しがいい。
if (isdigit(c) != 0) は無意味。

>   best_score = 0;
>   for (candidate = *candidates; candidate; candidates++) {
>     score = 0;
>     for (cp = candidate; *cp; cp++) {
>       if (*cp == ' ')
>         score = -1;
>     }
>     /*
>      * An inequality expression should always be written as
>      * (lesser < greater) order regardless of which side is the
>      * subject. It helps visualizing the numeric positions as a number
>      * line in an intuitive interpretation, especially in a range
>      * comparison as follows.
>      *
>      * Ruby: (worst..best) === n
>      * C:    (worst <= n && n <= best)
>      */
>     if (0 <= score)
>       score = (*evaluate)(candidate);
>     if (best_score <= score)
>       selected = candidate;
>   }

反対。
if (a > 0)
  positive;
if (a < 0)
  negative;
else
  perror(NULL);
みたいに、処理を切り分ける判断の主体をはっきりさせて書いた方がわかりやす
い。こともある。主体がころころ場所を変わらない方が機械的に条件式を認識で
きる。一方で、単純な一変数の判定でない場合は数直線的に並べた方がいいこと
もある。どっちか一方に固定するのは良くない。
ところで C0 <= x && x <= C1 は云わずもがなかと。

>    * Use `!' for tests even if it's not a boolean.
>    * E.g. use "if (!*p)", not "if (*p == '\0')".
>    *      use "if (!p)",  not "if (p == NULL)".

Duplicate.

>    * DO NOT cast a pointer in C++-style.
>    * E.g. use "(int *)p", not "(int*)p"

やりすぎ。どっちの表記も意味を正確にあらわしてるし、どっちで書いても間違
いにもつながらないし、どうせ () の方が視覚的にも優先度が高い。

>    * Do not use C++ style '0' for a NULL pointer.

何故? if (fp) 式の記述を許してるんだから当然 NULL == 0 は意識するでしょ
う。

>   /* Second level indents are also two spaces. */
>   while (cnt < 20)
>     z = a + really + long + statement + that + needs + two lines +
>       gets + indented + four + spaces + on + the + second +
>       and + subsequent + lines;

s/two lines/two + lines/   s/four/two/   :p

>   /*
>    * a return statement at end of a function should be separated by a
>    * blank line.

意味ないと思います。特に反対でもありませんが。
```

http://c2.com/cgi/wiki?CopyAndPasteProgramming

http://lists.sourceforge.jp/mailman/archives/anthy-dev/2005-September/002387.html
