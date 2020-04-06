# Документация

Здесь описаны функции и структуры для использования языка программирования **Gentee** в проектах на **Golang**.

* [type Custom](reference.md#type-custom)
* [type EmbedItem](reference.md#type-embed-item)
* [type Settings](reference.md#type-settings)
* [Customize\(custom \*Custom\) error](reference.md#customize-custom-custom-error)
* [New\(\) \*Gentee](reference.md#new-gentee)
* [\(g \*Gentee\) Compile\(input, path string\) \(\*Exec, int, error\)](reference.md#g-gentee-compile-input-path-string-exec-int-error)
* [\(g \*Gentee\) CompileAndRun\(filename string\) \(interface{}, error\)](reference.md#g-gentee-compileandrun-filename-string-interface-error)
* [\(g \*Gentee\) CompileAndRun\(filename string\) \(\*Exec, int, error\)](reference.md#g-gentee-compilefile-filename-string-exec-int-error)
* [\(exec \*Exec\) Run\(settings Settings\) \(interface{}, error\)](reference.md#exec-exec-run-settings-settings-interface-error)
* [Version\(\) string](reference.md#version-string)

## Типы

### type Custom

Тип _Custom_ служит для дополнительной настройки компилятора и виртуальной машины. Передается при вызове функции **Customize**.

* **Embedded** \[\]EmbedItem - массив дополнительных функций для стандартной библиотеки.

### type EmbedItem

Тип _EmbedItem_ описывает функцию, подключаемую к стандартной библиотеки. Используется в типе **Custom**.

* **Prototype** string - описание функции на языке Gentee. Например, _myfunc\(str,int\) int_.
* **Object** interface{} - соответствующая golang функция.

### type Settings

Тип _Settings_ служит для указания дополнительных параметров при запуске байт-кода в методе **Run**.

* **CmdLine** \[\]string - массив параметров командной строки.
* **Input** \[\]byte - предопределенный стандартный ввод (stdin). Может использоваться, например, в функции [ReadString](/stdlib/console.md#readstring-str-text-str).
* **Cycle** uint64 - максимальное количество итераций в цикле. По умолчанию, равно 16000000.
* **Depth** uint32 - максимальная вложенность исполняемых блоков. Ограничивает глубину рекурсии. По умолчанию, равно 1000.
* **SysChan** chan int - канал для отправки команд *SysSuspend* (1), *SysResume* (2), *SysTerminate* (3). Позволяет управлять выполнением скрипта извне.
  * *SysSuspend* - приостановить работу скрипта и всех потоков.
  * *SysResume* - возобновить работу скрипта и всех потоков.
  * *SysTerminate* - завершить работу скрипта и всех потоков.

``` go
    settings.SysChan = make(chan int)
    go func() {
        _, err = exec.Run(settings)
    }()
    settings.SysChan <- gentee.SysTerminate
```

## Функции и методы

### Customize\(custom \*Custom\) error

Функция _Customize_ служит для [дополнительной настройки компилятора](customize.md) и виртуальной машины. Она должна вызываться раньше всех функций. Функция возвращает значение ошибки.

### New\(\) \*Gentee

Функция _New_ создает рабочее пространство для компиляции исходного кода.

### \(g \*Gentee\) Compile\(input, path string\) \(\*Exec, int, error\)

Функция _Compile_ компилирует скрипт переданный в _input_. В параметре _path_ можно указать путь к скрипту. Функция возвращает структуру с байт-кодом, номер модуля и значение ошибки.

### \(g \*Gentee\) CompileAndRun\(filename string\) \(interface{}, error\)

Функция _CompileAndRun_ компилирует скрипт из файле _filename_ и выполняет его. Функция возвращает результат выполнения скрипта и значение ошибки.

### \(g \*Gentee\) CompileFile\(filename string\) \(\*Exec, int, error\)

Функция _CompileFile_ компилирует скрипт из файла _filename_. Функция возвращает структуру с байт-кодом, номер модуля и значение ошибки.

### \(exec \*Exec\) Run\(settings Settings\) \(interface{}, error\)

Функция _Run_ выполняет байт-код из структуры _exec_. В параметре _settings_ можно указать дополнительные настройки. Функция возвращает результат выполнения скрипта и значение ошибки.

### Version\(\) string

Функция _Version_ возвращает номер текущей версии языка.

