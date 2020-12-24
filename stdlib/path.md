# Путь

Здесь описаны функции для работы с путями разделяемых слешами.

* [AbsPath\( str path \) str](path.md#abspath-str-path-str)
* [BaseName\( str path \) str](path.md#basename-str-path-str)
* [Dir\( str path \) str](path.md#dir-str-path-str)
* [Ext\( str path \) str](path.md#ext-str-path-str)
* [JoinPath\( str path... \) str](path.md#joinpath-str-path-str)
* [MatchPath\( str pattern, str path \) bool](path.md#matchpath-str-pattern-str-path-bool)
* [Path\( finfo fi \) str](path.md#path-finfo-fi-str)

## Функции

### AbsPath\(str path\) str

Функция _AbsPath_ возвращает абсолютное представление пути.

### BaseName\(str path\) str

Функция _BaseName_ возвращает последний элемент пути. Если есть последний слеш, то он удаляется. Если путь пустой, то возвращается ".".

### Dir\(str path\) str

Функция _Dir_ возвращает путь, исключая последний элемент. Как правило, это путь директории.

### Ext\(str path\) str

Функция _Ext_ возвращает расширение файла. Расширение возвращается без точки.

### JoinPath\(str path...\) str

Функция _JoinPath_ объединяет все указанные пути в один путь, вставляя соответствующий разделитель, где он необходим.

### MatchPath\(str pattern, str path\) bool

Функция _MatchPath_ проверяет, подходит ли данное имя к указанному шаблону. Функция проверяет шаблон полностью для указанного пути, а не для подстроки. Вы можете в качестве шаблона использовать регулярное выражение. Для этого, добавьте в начало и конец символ */*.

* '\*' - любая последовательность, кроме символа разделителя
* '?' - любой одиночный символ, кроме символа разделителя

```text
MatchPath(`*.txt`, `myfile.txt`)       // true
MatchPath(`?a?.pdf`, `1ab.pdf`)        // true
MatchPath(`/home/ak/my.pdf`, `*.pdf`)         // false
MatchPath(`/home/ak/my.pdf`, `/home/*/my.*`)  // true
MatchPath(`/\/user\//`, `/home/user/myfile`) // true
```

### Path\(finfo fi\) str

Функция _Path_ объединяет поля *Name* и *Dir* в переменной типа *finfo* и возвращает полученный путь.
