# Рантайм

Здесь описаны функции для работы с виртуальной машиной во время выполнения скрипта.

* [error\( int id, str text, anytype pars... \)](runtime.md#error-int-id-str-text-anytype-pars)
* [ErrID\( error err \) int](runtime.md#errid-error-err-int)
* [ErrText\( error err \) str](runtime.md#errtext-error-err-str)
* [ErrTrace\( error err \) arr.trace](runtime.md#errtrace-error-err-arr-trace)
* [exit\( int code \)](runtime.md#exit-int-code)
* [Progress\( int id inc \)](runtime.md#progress-int-id-inc)
* [ProgressEnd\( int id \)](runtime.md#progressend-int-id)
* [ProgressStart\( int total ptype, str src dest \) int](runtime.md#progressstart-int-total-ptype-str-src-dest-int)
* [Trace\(\) arr.trace](runtime.md#trace-arr-trace)

## Типы

### trace

Тип _trace_ служит для хранения информации о вызове функции и имеет следующие поля:

* **str Path** - имя файла
* **str Entry** - текущая функция
* **str Func** - вызываемая функция
* **int Line** - строка в исходном коде
* **int Pos** - позиция в строке, где произошёл вызов

## Функции

### error\(int id, str text, anytype pars...\)

Функция _error_ генерирует ошибку времени выполнения скрипта.

* _id_ - код ошибки,
* _text_ - текст ошибки,
* _pars_ - необязательные параметры. Если они указаны, то _text_ должен содержать соответствующий шаблон

  как в функции [Format](https://gentee.github.io/docs-gentee-ru/stdlib/string#formatstr-s-anytype-args-str).

```go
    error(10, `Error message %{ 10 }`)
    error(10, `Error message %d`, 10)
```

### ErrID\(error err\) int

Функция _ErrID_ возвращает идентификатор ошибки _err_. Эта функция может использоваться внутри конструкции **try-catch** для обработки ошибок.

```go
run {
  try {
    .....
    error(101, `oooops`)
  }
  catch err {
    if ErrID(err) == 101 {
      recover
    } elif ErrID(err) < 100 {
      retry
    }
  }
}
```

### ErrText\(error err\) str

Функция _ErrText_ возвращает текст ошибки _err_. Эта функция может использоваться внутри конструкции **try-catch** для обработки ошибок.

### ErrTrace\(error err\) arr.trace

Функция _ErrTrace_ возвращает стек вызовов функций на момент возникновения ошибки _err_. Эта функция может использоваться внутри конструкции **try-catch** для обработки ошибок.

### exit\(int code\)

Функция _exit_ прекращает работу скрипта. Функция может быть вызвана в любом потоке. Скрипт возвращает значение _code_.

```go
func ok(int par) int {
  if par == 0 : exit(0)
  return 3 * par
}
run int {
  int sum
  for i in 10..-10 {
    sum += ok(i)
  }
  return sum
}
```

### Progress\( int id inc \)

Функция _Progress_ увеличивает величину счётчика процесса на значение параметра _inc_. _id_ - идентификатор прогресс-бара возвращённый функцией _ProgressStart_. Функция _Progress_ вызывает Go функцию _ProgressFunc_, которая должна быть определена в настройках при запуске скрипта.

``` go
  int total = 200
  int prog = ProgressStart(total, 100, `counter`, ``)
  for i in 1..5 {
    Progress(prog, 40)
  }
  ProgressEnd(prog)
```

### ProgressEnd\( int id \)

Функция _ProgressEnd_ удаляет счётчик процесса с идентификатором _id_.

### ProgressStart\( int total ptype, str src dest \) int

Функция _ProgressStart_ создаёт счётчик процесса и возвращает его идентификатор. _total_ - максимальная величина счётчика. _ptype_ - тип счётчика, может быть любое число. _src_ - имя источника. _dest_ - имя целевого объекта. Функции для работы с прогрессом-баром ничего не отображают, они вызывают функцию _ProgressFunc_, которая должна быть определена в [настройках](/golang/reference.md) при запуске скрипта. В функции _ProgressFunc_ вы можете отображать состояние процесса удобным для вас способом. После окончания работы с данным счётчиком необходимо вызвать функцию _ProgressEnd_ для его удаления.

### Trace\(\) arr.trace

Функция _Trace_ возвращает стек вызовов функций.

