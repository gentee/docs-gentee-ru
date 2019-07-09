---
nav: tocru
---

# Процесс

Здесь описаны операторы и функции для работы с процессами и приложениями. Функции _Args_ и _ArgCount_ работают с командной строкой любого формата. Для корректной работы остальных _Arg.._ функций необходимо, чтобы командная строка имела следующий формат.

```text
CmdLine = [ CmdOptions ] ["-"] [ CmdParameters ]
CmdParameters = { CmdParameter }
CmdParameter = ParamWithoutSpace | "Param With Spaces" | 'Param With Spaces'
CmdOptions = {CmdOption}
CmdOption = "-" | "--" {letter} [ CmdOptionValue | CmdOptionValues ]
CmdOptionValue = "=" | ":" CmdParameter
CmdOptionValues = " " CmdParameters
```

```text
-p="my value" --flag - one two three
-i:10 -n:Bob "one par" two three
--ext "*.txt" .js .html -o=/home/ak/dest /home/ak/in1 /home/ak/in2
```

* [Arg\( str name \) str](process.md#argstr-name-str)
* [Arg\( str name, str def \) str](process.md#argstr-name-str-def-str)
* [Arg\( str name, int def \) int](process.md#argstr-name-int-def-int)
* [ArgCount\(\) int](process.md#argcount-int)
* [Args\(\) arr.str](process.md#args-arrstr)
* [Args\( str name \) arr.str](process.md#argsstr-name-arrstr)
* [ArgsTail\(\) arr.str](process.md#argstail-arrstr)
* [IsArg\( str name \) bool](process.md#isargstr-name-bool)
* [Open\( str path \)](process.md#openstr-path)
* [OpenWith\( str app, str path \)](process.md#openwithstr-app-str-path)

## Операторы

| Operator | Result | Description |
| :--- | :--- | :--- |
| **$** command line |  | Запустить командную строку. |
| str = **$** command line |  | Запустить командную строку и возвратить её вывод. |

## Функции

### Arg\(str name\) str

Функция _Arg_ возвращает значение параметра с указанным именем. Если параметр не был указан при запуске скрипта, то возвратится пустая строка. В имени параметра можно не указывать начальный символ **-**.

### Arg\(str name, str def\) str

Функция _Arg_ возвращает значение параметра с указанным именем **name**. Если параметр не был указан при запуске скрипта, то возвратится значение **def**. В имени параметра можно не указывать начальный символ **-**.

### Arg\(str name, int def\) int

Функция _Arg_ возвращает числовое значение параметра с указанным именем **name**. Если параметр не был указан при запуске скрипта, то возвратится число **def**. В имени параметра можно не указывать начальный символ **-**.

### ArgCount\(\) int

Функция _ArgCount_ возвращает количество параметров командной строки с которыми был запущен скрипт.

### Args\(\) arr.str

Функция _Args_ возвращает список всех параметров и опций командной строки с которыми был запущен скрипт.

### Args\(str name\) arr.str

Функция _Args_ возвращает список значений параметра с именем **name**. В имени параметра можно не указывать начальный символ **-**.

```text
// --ext .txt .js .html -o=/home/ak/dest /home/ak/in1 /home/ak/in2
list = Args(`--ext`) 
// list == [.txt, .js, .html]
```

### ArgsTail\(\) arr.str

Функция _ArgsTail_ возвращает список параметров командной строки после опций. Можно явно указать начало таких параметров с помощью **-**.

```text
// --ext .txt .js .html -o=/home/ak/dest /home/ak/in1 /home/ak/in2
list = ArgsTail() // list == [/home/ak/in1, /home/ak/in2]

// -i=false - val0 -value1 "value 2" 
list = ArgsTail() // list == [val0, -value1, value 2]
```

### IsArg\(str name\) bool

Функция _IsArg_ возвращает _true_, если в командной строке имеется опция с указанным именем. В противном случае, возвращается _false_. В имени параметра можно не указывать начальный символ **-**.

### Open\(str path\)

Функция _Open_ открывает файл, директорию или URI адрес приложением по умолчанию для объектов данного типа. Скрипт не ожидает завершения работы.

### OpenWith\(str app, str path\)

Функция _OpenWith_ открывает файл, директорию или URI адрес в указанном приложении. Скрипт не ожидает завершения работы.

