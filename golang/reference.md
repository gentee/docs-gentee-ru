# Документация

Здесь описаны функции и структуры для использования языка программирования **Gentee** в проектах на **Golang**.

* [type Custom](reference.md#type-custom)
* [type EmbedItem](reference.md#type-embed-item)
* [type Settings](reference.md#type-settings)
* [type Progress](reference.md#type-progress)
* [Customize\(custom \*Custom\) error](reference.md#customize-custom-custom-error)
* [New\(\) \*Gentee](reference.md#new-gentee)
* [\(g \*Gentee\) Compile\(input, path string\) \(\*Exec, int, error\)](reference.md#g-gentee-compile-input-path-string-exec-int-error)
* [\(g \*Gentee\) CompileAndRun\(filename string\) \(interface{}, error\)](reference.md#g-gentee-compileandrun-filename-string-interface-error)
* [\(g \*Gentee\) CompileAndRun\(filename string\) \(\*Exec, int, error\)](reference.md#g-gentee-compilefile-filename-string-exec-int-error)
* [\(exec \*Exec\) Run\(settings Settings\) \(interface{}, error\)](reference.md#exec-exec-run-settings-settings-interface-error)
* [Gentee2GoType\(val interface{}, vtype... string\) interface{}](reference.md#gentee-2-gotype-val-interface-vtype-string-interface)
* [Go2GenteeType\(val interface{}, vtype... string\) \(interface{}, error\)](reference.md#go-2-genteetype-val-interface-vtype-string-interface-error)
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
* **Stdin** \*os.File - свой собственный стандартный ввод.
* **Stdout** \*os.File - свой собственный стандартный вывод.
* **Stderr** \*os.File - свой собственный вывод для ошибок.
* **Input** \[\]byte - предопределенный стандартный ввод (stdin). Может использоваться, например, в функции [ReadString](/stdlib/console.md#readstring-str-text-str).
* **Cycle** uint64 - максимальное количество итераций в цикле. По умолчанию, равно 16000000.
* **Depth** uint32 - максимальная вложенность исполняемых блоков. Ограничивает глубину рекурсии. По умолчанию, равно 1000.
* **SysChan** chan int - канал для отправки команд *SysSuspend* (1), *SysResume* (2), *SysTerminate* (3). Позволяет управлять выполнением скрипта извне.
  * *SysSuspend* - приостановить работу скрипта и всех потоков.
  * *SysResume* - возобновить работу скрипта и всех потоков.
  * *SysTerminate* - завершить работу скрипта и всех потоков.
* **IsPlayground** bool - присвойте *true*, если хотите запустить скрипт в безопасном режиме [песочницы](playground.md).
* **Playground** Playground - настройки режима песочницы.
  * *Path*  string - путь к временной директории для записи и чтения файлов. Если не указан, то будет будет создана поддиректория во временной директории.
  * *AllSizeLimit* int64 - суммарный размер файлов. По умолчанию, 10 MB.
  * *FilesLimit* int - максимальное количество файлов. По умолчанию, 100.
  * *SizeLimit* int64 - максимальный размер файла. По умолчанию, 5 MB.
* **ProgressFunc** gentee.ProgressFunc - функция для отображения процесса копирования, скачивания и т.д., например, в виде прогресс-бара. Функция должна иметь следующий тип:  
_func MyProgress(progress *gentee.Progress) bool_  
и возвращать *true*. Тип *Progress* описан ниже.

``` go
    settings.SysChan = make(chan int)
    go func() {
        _, err = exec.Run(settings)
    }()
    settings.SysChan <- gentee.SysTerminate
```

### type Progress

Тип _Progress_ служит для отображения процесса копирования, скачивания. Переменная этого типа передается в функцию _ProgressFunc_ и имеет следующие поля:

* **ID uint32** - уникальный идентификатор.
* **Type int32** - тип процесса.
  * *ProgressCopy (0)* - копирование.
  * *ProgressDownload (1)* - скачивание.
  * *ProgressCompress (2)* - сжатие.
  * *ProgressDecompress (3)* - распаковка.
* **Status int32** - статус.
  * *ProgStatusStart (0)* - начало процесса.
  * *ProgStatusActive (1)* - процесс идёт.  
  * *ProgStatusEnd (2)* - процесс закончен.  
* **Total int64** - общий размер.
* **Current int64** - текущий размер.
* **Source string** - источник процесса.
* **Dest string** - целевой объект процесса.
* **Ratio float64** - отношение *Current/Total*. Для получения процентов необходимо умножить на 100.
* **Custom interface{}** - служит для хранения любой дополнительной информации.

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

### Gentee2GoType\(val interface{}, vtype... string\) interface{}

Функция _Gentee2GoType_ конвертирует переменную в стандартные типы Go. Во втором параметре можно указать тип Gentee переменной. Например, _arr.bool_. В этом случае, вы получите массив переменных типа _bool_, а не _int64_. Вы можете использовать эту функцию, в ваших встраиваемых функциях.

Таблица соответствия типов

| Gentee тип | Получаемый тип | Возвращаемый тип (vtype)
| :--- | :--- | :--- |
| int | int64 | int64
| bool | int64 | bool ("bool")
| char | int64 | rune ("rune")
| float | float64 | float64
| str | string | string
| arr | *core.Array | []interface{}
| buf | *core.Buffer | []byte
| map | *core.Map | map[string]interface{}
| set | *core.Set | []byte
| struct type | *core.Struct | map[string]interface{}
| obj | *core.Obj | interface{}

```go
func cnv1(in *core.Map) (*core.Map, error) {
  my := gentee.Gentee2GoType(in).(map[string]interface{})
  for key, a := range my {
    for i, v := range a.([]interface{}) {
      a.([]interface{})[i] = v.(int64) + 1
    }
    delete(my, key)
    my[key+`2`] = a
  }
  ret, err := gentee.Go2GenteeType(my)
  return ret.(*core.Map), err
}
```

### Go2GenteeType\(val interface{}, vtype... string\) \(interface{}, error\)

Функция _Go2GenteeType_ конвертирует стандартный тип Go в тип Gentee. Во втором параметре можно указать тип Gentee переменной. Например, _set_, если вы хотите сконвертировать _[]byte_ в *core.Set. Вы можете использовать эту функцию, в ваших встраиваемых функциях.

Таблица соответствия типов

| Gentee тип | Получаемый Go тип | Возвращаемый тип (vtype)
| :--- | :--- | :--- |
| int | all int & uint | int64
| bool | bool | int64
| char | rune | int64
| float | float64 | float64
| str | string | string
| arr | []interface{} | *core.Array
| buf | []byte | *core.Buffer
| set | []byte | *core.Set ("set")
| map | map[string]interface{} | *core.Map
| obj | interface{} | *core.Obj ("obj")

```go
func cnv5(in *core.Set) (*core.Set, error) {
  my := gentee.Gentee2GoType(in).([]byte)
  for i, b := range my {
    if i > 10 {
      break
    }
    if b == 0 {
      my[i] = 1
    } else {
      my[i] = b - 1
    }
  }
  ret, err := gentee.Go2GenteeType(my, `set`)
  return ret.(*core.Set), err
}
```

### Version\(\) string

Функция _Version_ возвращает номер текущей версии языка.

