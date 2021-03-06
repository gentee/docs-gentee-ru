# Строки

Здесь описаны операторы и функции для работы со строками \(тип **str**\).

* [bool\( str s \) bool](string.md#bool-str-s-bool)
* [float\( str s \) float](string.md#float-str-s-float)
* [int\( str s \) int](string.md#int-str-s-int)
* [Find\( str s, str substr \) int](string.md#find-str-s-str-substr-int)
* [Format\( str s, anytype args... \) str](string.md#format-str-s-anytype-args-str)
* [HasPrefix\( str s, str prefix \) bool](string.md#hasprefix-str-s-str-prefix-bool)
* [HasSuffix\( str s, str suffix \) bool](string.md#hassuffix-str-s-str-suffix-bool)
* [Left\( str s, int i \) string](string.md#left-str-s-int-i-str)
* [Lines\( str s \) arr.str](string.md#lines-str-s-arr-str)
* [Lower\( str s \) string](string.md#lower-str-s-str)
* [Repeat\( str s, int count \) str](string.md#repeat-str-s-int-count-str)
* [Replace\( str s, str old, str new \) str](string.md#replace-str-s-str-old-str-new-str)
* [Right\( str s, int i \) string](string.md#right-str-s-int-i-str)
* [Size\( int size, str format \) string](string.md#size-int-size-str-format-str)
* [Split\( str s, str sep \) arr.str](string.md#split-str-s-str-sep-arr-str)
* [Substr\( str s, int off, int length \) str](string.md#substr-str-s-int-off-int-length-str)
* [Trim\( str s, str cutset \) str](string.md#trim-str-s-str-cutset-str)
* [TrimLeft\( str s, str cutset \) str](string.md#trimleft-str-s-str-cutset-str)
* [TrimRight\( str s, str cutset \) str](string.md#trimright-str-s-str-cutset-str)
* [TrimSpace\( str s \) str](string.md#trimspace-str-s-str)
* [Upper\( str s \) string](string.md#upper-str-s-str)

## Операторы

| Оператор | Результат | Описание |
| :--- | :--- | :--- |
| str **+** str | str | Слияние двух строк. |
| **\*** str | int | Получить длину строки. |
| str **?** | bool | Вызов *bool(str)*. |
| **\|** str | str | Этот унарный оператор удаляет пробельные символы в начале, в конце строки и рядом с символами перевода строки. |
| str **==** str | bool | Возвращает _true_ если две строки равны и _false_, в противном случае. |
| str **&gt;** str | bool | Возвращает _true_ если первая строка больше второй и _false_, в противном случае. |
| str **&lt;** str | bool | Возвращает _true_ если первая строка меньше второй и _false_, в противном случае. |
| str **!=** str | bool | Возвращает _true_ если две строки не равны и _false_, в противном случае. |
| str **&gt;=** str | bool | Возвращает _true_ если первая строка больше или равна второй и _false_, в противном случае. |
| str **&lt;=** str | bool | Возвращает _true_ если первая строка меньше или равна второй и _false_, в противном случае. |
| str **=** str | str | Присваивание строки. |
| str **=** int | str | Конвертирует целое число в строку и присваивает её переменной. |
| str **=** bool | str | Присваивает переменной "true" или "false". |
| str **+=** str | str | Добавляет к строковой переменной строку. |
| str **\[** int **\]** | int | Установить/получить уникодный символ по индексу. |

## Функции

### bool\(str s\) bool

Функция _bool_ возвращает _false_, если строка пустая, равна "0" или "false", в противном случае, возвращается _true_.

### float\(str s\) float

Функция _float_ преобразует строку в число типа _float_. Если строка имеет неверный формат, то возвращается ошибка.

### int\(str s\) int

Функция _int_ преобразует строку в число типа _int_. Если строка имеет неверный формат, то возвращается ошибка.

### Find\(str s, str substr\) int

Функция _Find_ возвращает смещение первого вхождения подстроки _substr_ в строке _s_, или -1, если _substr_ отсутствует в строке _s_.

### Format\(str s, anytype args...\) str

Функция _Format_ форматирует строку в соответствии со спецификатором _s_ и возвращает результирующую строку. Имеются следующие управляющие команды:

#### Общие

* **%v** - значение в формате по умолчанию
* **%%** - знак процента 

#### bool

* **%t** -    слово true или false

#### int

* **%b** - по основанию 2
* **%c** - соответствующий символ Unicode
* **%d** - по основанию 10. Это формат по умолчанию для _int_.
* **%o** - по основанию 8
* **%x** - по основанию 16, с нижним регистром a-f
* **%X** - по основанию 16, с верхним регистром A-F
* **%U** - формат    Unicode: U+1234

#### float

* **%e** - научная запись, например -1.234456e+78
* **%E** - научная запись, например -1.234456E+78
* **%f** - десятичная точка без экспоненты, например 123.456. Вы можете указать общую ширину и мантиссу _%\[width\].\[precision\]f_ - _%8.2f, %.3f, %7f_.
* **%g** - %e для большой экспоненты, и %f в противном случае. Это формат по умолчанию для _float_.

#### str

* **%s** - формат по умолчанию для строк.
* **%x** - по основанию 16 в нижнем регистре, два символа на 1 байт.
* **%X** - по основанию 16 в верхнем регистре, два символа на 1 байт.

Вы можете указать i-ый аргумент в форматируемой строке подобно этому - _Format\("%d %\[1\]d %\[1\]d", 10\)_

```text
arr.int mya = {1,2,3}
time t
Format(`%s %v %v %g %6.2[4]f`, `ok`, mya, Now(t), 99.0 + 1.)
```

### HasPrefix\(str s, str prefix\) bool

Функция _HasPrefix_ возвращает _true_, если строка _s_ начинается со строки _prefix_.

### HasSuffix\(str s, str suffix\) bool

Функция _HasSuffix_ возвращает _true_, если строка _s_ заканчивается строкой _suffix_.

### Left\(str s, int i\) str

Функция _Left_ возвращает подстроку из первых _i_ символов строки _s_.

### Lines\(str s\) arr.str

Функция _Lines_ разбивает строку _s_ на подстроки по символам перевода строки. Все подстроки добавляются в возвращаемый массив строк.

### Lower\(str s\) str

Функция _Lower_ приводит копию строки _s_ к нижнему регистру и возвращает её.

### Repeat\(str s, int count\) str

Функция _Repeat_ возвращает новую строку состоящую из _count_ повторений строки _s_.

### Replace\(str s, str old, str new\) str

Функция _Replace_ возвращает копию строки _s_ со всеми подстроками _old_ замененными на строку _new_.

### Right\(str s, int i\) str

Функция _Right_ возвращает подстроку из последних _i_ символов строки _s_.

### Size\(int size, str format\) str

Функция _Size_ возвращает округленный размер в виде строки. В параметре _format_ укажите шаблон вывода для десятичного числа с плавающей точкой и строки. Если _format_ равен пустой строке, то используется формат *%.2f%s*.

``` go
Print( Size(956348901, `%.1f %s `) + Size(62, `%[2]s%.2[1]f `) + Size(123789, ``))
// 912.0 MB B62 120.89KB
```

### Split\(str s, str sep\) arr.str

Функция _Split_ разбивает строку _s_ на подстроки разделенные строкой _sep_. Все подстроки добавляются в возвращаемый массив строк.

### Substr\(str s, int off, int length\) str

Функция _Substr_ возвращает подстроку _s_ с указанным смещением и длиной.

### Trim\(str s, str cutset\) str

Функция _Trim_ возвращает подстроку строки _s_ с удалёнными начальными и конечными символами, которые содержатся в строке _cutset_.

### TrimLeft\(str s, str cutset\) str

Функция _TrimLeft_ возвращает подстроку строки _s_ с удалёнными начальными символами, которые содержатся в строке _cutset_.

### TrimRight\(str s, str cutset\) str

Функция _TrimRight_ возвращает подстроку строки _s_ с удалёнными конечными символами, которые содержатся в строке _cutset_.

### TrimSpace\(str s\) str

Функция _TrimSpace_ возвращает подстроку строки _s_ с удалёнными начальными и конечными пробельными символами.

### Upper\(str s\) str

Функция _Upper_ приводит копию строки _s_ к верхнему регистру и возвращает её.

