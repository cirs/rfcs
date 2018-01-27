- Feature Name: c_locale_ctype
- Start Date: 2018-01-25
- RFC PR: (leave this empty)
- Cirs Issue: (leave this empty)

# Summary
[Summary]: #summary

Introduce the functions given in §7.4 Character handling &amp;ctype.h>.

# Motivation
[Motivation]: #motivation

The library needs to get going from somewhere and `<ctype.h>` functions are
easiest to implement, for the `"C"` locale.

# Guide-level explanation
[Guide-level explanation]: #guide-level-explanation

The following `extern "C"` functions are introduced in the `::ctype` module:

## Character classification functions
[Character classification functions]: #character-classification-functions

```C
int isalnum(int);
int isalpha(int);
int isblank(int);
int iscntrl(int);
int isdigit(int);
int isgraph(int);
int islower(int);
int isprint(int);
int ispunct(int);
int isspace(int);
int isupper(int);
int isxdigit(int);
```

## Character case mapping functions
[Character case mapping functions]: #character-case-mapping-functions

```C
int tolower(int);
int toupper(int);
```

## Configuration
[Configuration]: #configuration

In addition the features `ctype` and `c_locale_ctype` are also introduced.

# Reference-level explanation
[Refernce-level explanation]: #reference-level-explanation

This RFC only covers the tests performs with the assumation that the locale is
"C". Other locales are not within the scope this RFC and should be provided as
separate RFCs that provides the specification for the specific locales.

## Standard Character Set
[Standard Character Set]: #standard-character-set

According to §5.2.1 Character sets, the following characters are considered
under standard characters:
1. Uppercase letters:
> `A` `B` `C` `D` `E` `F` `G` `H` `I` `J` `K` `L` `M`
> `N` `O` `P` `Q` `R` `S` `T` `U` `V` `W` `X` `Y` `Z`
2. Lowercase letters:
> `a` `b` `c` `d` `e` `f` `g` `h` `i` `j` `k` `l` `m`
> `n` `o` `p` `q` `r` `s` `t` `u` `v` `w` `x` `y` `z`
3. Decimal digits:
> `0` `1` `2` `3` `4` `5` `6` `7` `8` `9`
4. Graphic characters:
> `!` `"` `#` `%` `&` `'` `(` `)` `*` `+` `,` `-` `.` `/` `:`
> `;` `<` `=` `>` `?` `[` `\` `]` `^` `_` `{` `|` `}` `~`
5. Hexadecimal characters:
> `0` `1` `2` `3` `4` `5` `6` `7` `8` `9`
> `A` `B` `C` `D` `E` `F`
> `a` `b` `c` `d` `e` `f`

## Character Classification Set
[Character Classification Set]: #character-classification-set

 Character Range | `isalnum` | `isalpha` | `isblank` | `iscntrl` | `isdigit` | `isgraph` | `islower` | `isprint` | `ispunct` | `isspace` | `isupper` | `isxdigit`
:---------------:|:---------:|:---------:|:---------:|:---------:|:---------:|:---------:|:---------:|:---------:|:---------:|:---------:|:---------:|:----------:
 `0x00`..`0x08`  | 0         | 0         | 0         | 1         | 0         | 0         | 0         | 0         | 0         | 0         | 0         | 0
 `0x09`          | 0         | 0         | 1         | 1         | 0         | 0         | 0         | 0         | 0         | 1         | 0         | 0
 `0x0A`..`0x0D`  | 0         | 0         | 0         | 1         | 0         | 0         | 0         | 0         | 0         | 1         | 0         | 0
 `0x0E`..`0x1F`  | 0         | 0         | 0         | 1         | 0         | 0         | 0         | 0         | 0         | 0         | 0         | 0
 `0x20`          | 0         | 0         | 1         | 0         | 0         | 0         | 0         | 1         | 0         | 1         | 0         | 0
 `0x21`..`0x2F`  | 0         | 0         | 0         | 0         | 0         | 1         | 0         | 1         | 1         | 0         | 0         | 0
 `0x30`..`0x39`  | 1         | 0         | 0         | 0         | 1         | 1         | 0         | 1         | 0         | 0         | 0         | 1
 `0x3a`..`0x40`  | 0         | 0         | 0         | 0         | 0         | 1         | 0         | 1         | 1         | 0         | 0         | 0
 `0x41`..`0x46`  | 1         | 1         | 0         | 0         | 0         | 1         | 0         | 1         | 0         | 0         | 1         | 1
 `0x47`..`0x5A`  | 1         | 1         | 0         | 0         | 0         | 1         | 0         | 1         | 0         | 0         | 1         | 0
 `0x5B`..`0x60`  | 0         | 0         | 0         | 0         | 0         | 1         | 0         | 1         | 1         | 0         | 0         | 0
 `0x61`..`0x66`  | 1         | 1         | 0         | 0         | 0         | 1         | 1         | 1         | 0         | 0         | 0         | 1
 `0x67`..`0x7A`  | 1         | 1         | 0         | 0         | 0         | 1         | 1         | 1         | 0         | 0         | 0         | 0
 `0x7B`..`0x7E`  | 0         | 0         | 0         | 0         | 0         | 1         | 0         | 1         | 1         | 0         | 0         | 0
 `0x7F`          | 0         | 0         | 0         | 1         | 0         | 0         | 0         | 0         | 0         | 0         | 0         | 0

## Character Case Mapping Set
[Character Case Mapping Set]: #character-case-mapping-set

 Character Range | `tolower` | `toupper`
:---------------:|:---------:|:---------:
 `0x00`..`0x40`  | 0         | 0
 `0x41`..`0x5A`  | 1         | 0
 `0x5B`..`0x60`  | 0         | 0
 `0x61`..`0x7A`  | 0         | -1
 `0x7B`..`0x7F`  | 0         | 0

## Features
[Features]: #features

This RFC also introduces two features to be used as configuration options:

### `ctype`
[`ctype`]: #ctype

This feature brings `<ctype.h>` functions into scope. This however feature
does not specify behaviour of the functions.

### `c_locale_ctype`
[`c_locale_ctype`]: #c_locale_ctype

This feature allows running `<ctype.h>` with `"C"` locale, as defined above.
This feature depends on the feature [`ctype`].

# Drawbacks
[Drawbacks]: #drawbacks

None

# Rationale and alternatives
[Rationale and alternatives]: #rationale-and-alternatives

None

# Unresolved questions
[Unresolved questions]: #unresolved-questions

* [ ] Should we mark the functions as `#[unstable]` until a future RFC
introduces the `locale.h`?
* [ ] How do we deal with the undefined behaviour for invalid values.
* [ ] Should this RFC mandate checking for `EOF` right now for the functions.
