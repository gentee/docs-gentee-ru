---
nav: tocru
---

# Регулярные выражения

Здесь описаны функции для работы с регулярными выражениями.

* [FindRegExp\( str src, str re \) arr.arr.str](regexp.md#findregexpstr-src-str-re-arrarrstr)
* [Match\( str s, str re \) bool](regexp.md#matchstr-s-str-re-bool)
* [ReplaceRegExp\( str src, str re, str repl \) str](regexp.md#replaceregexpstr-src-str-re-str-repl-str)

## Функции

### FindRegExp\(str src, str re\) arr.arr.str

Функция _FindRegExp_ находит все вхождения регулярного выражения _re_ в указанной строке _src_. Функция возвращает массив массивов. Первый элемент в каждом из массивов содержит подстроку совпадающую с регулярным выражением.

```text
arr.arr.str a &= FindRegExp(`My email is xyz@example.com`, `(\w+)@(\w+)\.(\w+)`)
// a = { { `xyz@example.com`, `xyz`, `example`, `com`} }
a &= FindRegExp(`This is a test string`, `i.`)
// a = { { `is` }, {`is`}, {`in`} }
```

### Match\(str s, str re\) bool

Функция _Match_ определяет содержит ли данная строка вхождение указанного регулярного выражения.

```text
bool a = Match(`somethiabng striabnbg`, `a.b`)  // false
a = Match(`somethianbg string`, `a.b`) // true
```

### ReplaceRegExp\(str src, str re, str repl\) str

Функция _ReplaceRegExp_ находит все вхождения регулярного выражения _re_ в указанной строке _src_ и заменяет их на строку _repl_. В параметре _repl_ можно указывать _$i_ или _${i}_ для i-го подсовпадения.

```text
str s = ReplaceRegExp("This is a string", `i(.{2})`, "xyz") 
// Thxyzxyza strxyz
s = ReplaceRegExp(" email is xyz@example.com", `(\w+)@(\w+)\.(\w+)`, "${3}.${2}@zzz")
// email is com.example@zzz
```

