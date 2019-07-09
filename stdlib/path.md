

# Путь

Здесь описаны функции для работы с путями разделяемых слешами.

* [AbsPath\( str path \) str](path.md#abspathstr-path-str)
* [BaseName\( str path \) str](path.md#basenamestr-path-str)
* [Dir\( str path \) str](path.md#dirstr-path-str)
* [Ext\( str path \) str](path.md#extstr-path-str)
* [JoinPath\( str path... \) str](path.md#joinpathstr-path-str)
* [MatchPath\( str pattern, str path \) bool](path.md#matchpathstr-pattern-str-path-bool)

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

Функция _MatchPath_ проверяет, подходит ли данное имя к указанному шаблону. Функция проверяет шаблон полностью для указанного пути, а не для подстроки.

* '\*' - любая последовательность, кроме символа разделителя
* '?' - любой одиночный символ, кроме символа разделителя

```text
MatchPath(`*.txt`, `myfile.txt`)       // true
MatchPath(`?a?.pdf`, `1ab.pdf`)        // true
MatchPath(`/home/ak/my.pdf`, `*.pdf`)         // false
MatchPath(`/home/ak/my.pdf`, `/home/*/my.*`)  // true
```

