# Рантайм

Здесь описаны функции для работы с виртуальной машиной во время выполнения скрипта.

* [error\( int id, str text, anytype pars... \)](runtime.md#errorint-id-str-text-anytype-pars)
* [ErrID\( error err \) int](runtime.md#erriderror-err-int)
* [ErrText\( error err \) str](runtime.md#errtexterror-err-str)
* [ErrTrace\( error err \) arr.trace](runtime.md#errtraceerror-err-arrtrace)
* [Trace\(\) arr.trace](runtime.md#trace-arrtrace)

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

```text
    error(10, `Error message %{ 10 }`)
    error(10, `Error message %d`, 10)
```

### ErrID\(error err\) int

Функция _ErrID_ возвращает идентификатор ошибки _err_. Эта функция может использоваться внутри конструкции **try-catch** для обработки ошибок.

```text
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

### Trace\(\) arr.trace

Функция _Trace_ возвращает стек вызовов функций.

