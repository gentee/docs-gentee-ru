# Регулярные выражения

Здесь описаны функции для работы с регулярными выражениями.

* [FindFirstRegExp\( str src, str re \) arr.str](regexp.md#findfirstregexp-str-src-str-re-arr-str)
* [FindRegExp\( str src, str re \) arr.arr.str](regexp.md#findregexp-str-src-str-re-arr-arr-str)
* [Match\( str s, str re \) bool](regexp.md#match-str-s-str-re-bool)
* [RegExp\( str src, str re \) str](regexp.md#regexp-str-src-str-re-str)
* [ReplaceRegExp\( str src, str re, str repl \) str](regexp.md#replaceregexp-str-src-str-re-str-repl-str)

## Функции

### FindFirstRegExp\(str src, str re\) arr.str

Функция _FindFirstRegExp_ находит первое вхождение регулярного выражения _re_ в указанной строке _src_. Функция возвращает массив строк. Первый элемент содержит подстроку совпадающую с регулярным выражением, остальные элементы содержат значения групп **(...)**, если они определены в регулярном выражении.

```go
arr.str a &= FindFirstRegExp(`This45i33s a isi777s inis1i2sg`, `is(\d*)i(\d+)s`)
// a = {`is45i33s`, `45`, `33`}
```

### FindRegExp\(str src, str re\) arr.arr.str

Функция _FindRegExp_ находит все вхождения регулярного выражения _re_ в указанной строке _src_. Функция возвращает массив массивов. Первый элемент в каждом из массивов содержит подстроку совпадающую с регулярным выражением.

```go
arr.arr.str a &= FindRegExp(`My email is xyz@example.com`, `(\w+)@(\w+)\.(\w+)`)
// a = { { `xyz@example.com`, `xyz`, `example`, `com`} }
a &= FindRegExp(`This is a test string`, `i.`)
// a = { { `is` }, {`is`}, {`in`} }
```

### Match\(str s, str re\) bool

Функция _Match_ определяет содержит ли данная строка вхождение указанного регулярного выражения.

```go
bool a = Match(`somethiabng striabnbg`, `a.b`)  // false
a = Match(`somethianbg string`, `a.b`) // true
```

### RegExp\(str src, str re\) str

Функция _RegExp_ возвращает первое вхождение регулярного выражения _re_ в указанной строке _src_. Если соответствия не найдено, то возвращается пустая строка.

```go
  str input = "This is a string тестовое значение"
  ret = RegExp(input, `is (.{2})`) + RegExp(input, `е(.+?)е`)
  // isстово
```

### ReplaceRegExp\(str src, str re, str repl\) str

Функция _ReplaceRegExp_ находит все вхождения регулярного выражения _re_ в указанной строке _src_ и заменяет их на строку _repl_. В параметре _repl_ можно указывать _$i_ или _${i}_ для i-го подсовпадения.

```go
str s = ReplaceRegExp("This is a string", `i(.{2})`, "xyz") 
// Thxyzxyza strxyz
s = ReplaceRegExp(" email is xyz@example.com", `(\w+)@(\w+)\.(\w+)`, "${3}.${2}@zzz")
// email is com.example@zzz
```

