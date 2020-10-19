# Система

Здесь описаны общие системные функции.

* [GetEnv\( str name \) str](system.md#getenv-str-name-str)
* [SetEnv\( str name, bool|int|str val \)](system.md#setenv-str-name-bool-val)
* [UnsetEnv\( str name \)](system.md#unsetenv-str-name)

## Функции

### GetEnv\(str name\) str

Функция _GetEnv_ возвращает значение переменной окружения.

``` go
Print( GetEnv("PATH"))
// the same as
Print( $PATH )
```

### SetEnv\(bool|int|str name\)

Функция _SetEnv_ присваивает переменной окружения указанное значение.

``` go
SetEnv("MYVARB", true)
SetEnv("MYVARI", 101)
SetEnv("MYVAR", "Test value")
// the same as
$MYVARB = true
$MYVARI = 101
$MYVARI = "Test value"
```

### UnsetEnv\(str name\)

Функция _UnsetEnv_ удаляет переменную окружения.
