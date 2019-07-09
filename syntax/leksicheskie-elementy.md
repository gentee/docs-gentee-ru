---
nav: tocru
---

# Лексические элементы

Исходный код должен быть в кодировке UTF-8. Синтаксис описан с использованием расширенной формы Бэкуса-Наура.

```text
newline        = 0x0A
unicode_char = /* Unicode code point */
unicode_linechar  = /* Unicode code point except newline */ 
unicode_letter = /* a Unicode code point classified as "Letter" */
letter        = unicode_letter | "_"
decimal_digit = "0" … "9" 
octal_digit   = "0" … "7" 
hex_digit     = "0" … "9" | "A" … "F" | "a" … "f" 
decimals  = decimal_digit { decimal_digit }
exponent  = ( "e" | "E" ) [ "+" | "-" ] decimals
```

## Комментарии и замена символов

Имеются следующие типы комментариев и автоматически заменяемых символов

`// Однострочный комментарий`  
Однострочный комментарий начинается с двойного слеша `//` и заканчивается символом перевода строки _newline_.

`/* Общий комментарий */`  
Общий комментарий начинается с комбинации / _и заканчивается_ /. Такие комментарии могут вставляться где угодно.

`# Заголовок`  
В начале скрипта можно указать данные для использования в других программах. Такие комментарии должны идти подряд в каждой строке от начала скрипта. Можно не указывать '\#' в начале каждой строки, а вставить **\#\#\#** перед и после текста.

```text
#!/usr/local/bin/gentee
# первая строка может использоваться для запуска скрипта в Linux.
###
  desc = Description of the script
  result = ok
  var = value
###
```

**;**  
Символ перевода строки служит разделителем между выражениями и управляющими конструкциями. Точка с запятой заменяется на перевод строки. Таким образом, вы можете использовать точку с запятой, если вы хотите разместить несколько выражений на одной строке.

**:**  
Двоеточие заменяется на открывающую фигурную скобку и вставляется закрывающая фигурная скобка в конце текущей строки.

```text
// эти примеры эквивалентны
if a == 10 : a = b + c; c = d + e 

if a == 10 
{
   a = b + c
   c = d + e
}
```

## Идентификаторы

Идентификаторы - это имена, которые используются для обозначения переменных, типов, констант, функций и т.д.. Идентификатор определяется с помощью последовательности букв и цифр, но начинаться идентификатор должен с буквы.

```text
identifier = letter { letter | unicode_digit }
IdentifierList = identifier { identifier }
```

Имеется несколько предопределённых идентификаторов и ключевых слов. Следующие слова зарезервированы и не могут быть использованы в качестве идентификаторов.

### Ключевые слова

**catch const elif else false for func go if in local recover retry return run struct true try while**

### Предопределенные типы стандартной библиотеки

**arr bool buf char error finfo float int map range set str time trace thread**

## Литералы

Целочисленный литерал - это последовательность цифр представляющая целочисленное число \(константу\).

```text
decimal = ( "1" … "9" ) { decimal_digit } 
octal = "0" { octal_digit } .
hex = "0" ( "x" | "X" ) hex_digit { hex_digit } 
integer = decimal | octal | hex
float = decimals "." [ decimals ] [ exponent ] | decimals exponent
```

```text
0x34Fab
0722
19023862
0.123e+3
234.e-2
9.7732E-1
0.0177E+2
5e-2
```

Символьный _char_ литерал служит для идентификации Unicode символа. Вы можете указать один конкретный символ или последовательность символов начинающуюся с обратного слеша заключенные в одинарные кавычки. Последовательность символов с обратным слешем может иметь несколько форматов:

```text
'\r',  '\n',  '\t', '\"', '\'', '\\' 
\xa5 \x2B  (\x + two hex_digit)
\u03B1  (\u + four hex_digit)
\0371  (\0 + three octal_digit)
```

```text
byteVal  = octalStr | hexStr .
octalStr = `\` "0" octal_digit octal_digit octal_digit .
hexStr   = `\` "x" hex_digit hex_digit .
uShort   = `\` "u" hex_digit hex_digit hex_digit hex_digit .
uLong    = `\` "U" hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit .
escapedChar     = `\` ( "a" | "b" | "f" | "n" | "r" | "t" | "v" | `\` | `"` ) 
charLit         = "'" ( unicode_char | uShort | uLong | escapedChar | byteVal | `\'`) "'" .
```

Имеется два типа строковых литералов. 1. Строка в обратных кавычках может содержать любые символы. Если нужно указать обратную кавычку, то нужно удвоить её. 2. Строка в двойных кавычках также может содержать любые символы \(в том числе перенос строки\), но у неё имеется управляющий символ в виде обратной косой черты. Вы можете указывать после обратной косой черты следующие символы

```text
\a   U+0007 alert or bell  
\b   U+0008 backspace  
\f   U+000C form feed  
\n   U+000A newline  
\r   U+000D carriage return  
\t   U+0009 horizontal tab  
\v   U+000b vertical tab  
\\   U+005c backslash  
\"   U+0022 double quote
```

```text
stringLit         = stringBackQuote | stringDoubleQuote
stringBackQuote   = "`" { unicode_char | "%{" Expression "}" | "${" identifier "}" } "`"
stringDoubleQuote = `"` { unicode_char | uShort | uLong | escapedChar | byteVal | "\{" Expression "}" } `"`
```

В любой тип строки можно вставлять выражения. При этом тип выражения может быть любым, если имеется соответствующая функция приведения этого типа к строке. Выражения должны быть заключены в фигурные скобки со предшествующим знаком **%** \(для обратных кавычек\) или обратной косой чертой \(в случае двойных кавычек\).

```text
`10+20 equals %{10 + 20}. User name is "%{USERNAME}"`
"This is the first line.\r\nThis is \{ `the` + `second`} line."
```

