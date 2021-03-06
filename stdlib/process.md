# Процесс

Здесь описаны операторы и функции для работы с процессами и приложениями. Функции _Args_ и _ArgCount_ работают с командной строкой любого формата. Для корректной работы остальных _Arg.._ функций необходимо, чтобы командная строка имела следующий формат.

```go
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

* [Arg\( str name \) str](process.md#arg-str-name-str)
* [Arg\( str name, str def \) str](process.md#arg-str-name-str-def-str)
* [Arg\( str name, int def \) int](process.md#arg-str-name-int-def-int)
* [ArgCount\(\) int](process.md#argcount-int)
* [Args\(\) arr.str](process.md#args-arr-str)
* [Args\( str name \) arr.str](process.md#args-str-name-arr-str)
* [ArgsTail\(\) arr.str](process.md#argstail-arr-str)
* [IsArg\( str name \) bool](process.md#isarg-str-name-bool)
* [Open\( str path \)](process.md#open-str-path)
* [OpenWith\( str app, str path \)](process.md#openwith-str-app-str-path)
* [Run\( str cmd, str params... \)](process.md#run-str-cmd-str-params)
* [SplitCmdLine\( str cmdline \) arr.str](process.md#splitcmdline-str-cmdline-arr-str)
* [Start\( str cmd, str params... \)](process.md#start-str-cmd-str-params)

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

### Run\(str cmd, str params...\)

**Опциональные параметры**

* **buf stdin** - буфер, который будет передан приложению как стандартный ввод.
* **buf stdout** - буфер, в который будет записан стандартный вывод приложения.
* **buf stderr** - буфер, в который будет записан стандартный вывод ошибок приложения.

Функция _Run_ запуcкает указанную программу _cmd_ c параметрами и ожидает её окончание. Дополнительно, вы можете переопределить стандартный ввод и вывод.

```go
    buf dirout
    Run("dir", stdout: dirout)
    Run("bash", stdin: buf(
      |`echo "dirs"
        #comment    
        echo "%{str(dirout)}"`
    ))
```

### SplitCmdLine\(str cmdline\) arr.str

Функция _SplitCmdLine_ разбирает входящую строку с параметрами командной строки и возвращает массив параметров.

```go
run str {
    return SplitCmdLine(`param1 "second par" "qwert\"y" 100 'oo ps'
-lastparam`).Join(`=`)
}
// returns param1=second par=qwert"y=100=oo ps=-lastparam
```

### Start\(str cmd, str params...\)

**Опциональные параметры**

* **buf stdin** - буфер, который будет передан приложению как стандартный ввод.

Функция _Start_ запуcкает указанную программу _cmd_ c параметрами и выполняет скрипт дальше. Дополнительно, вы можете передать буфер в качестве стандартного ввода.

```go
    Start("echo", "hello, world!")
    Start("bash", stdin: buf(
      |`./myscript1.sh
        ./myscript2.sh`
    ))
```

