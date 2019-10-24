# Сеть

Здесь описаны функции для работы с сетью/интернетом.

* [Download\( str url, str filename \) int](network.md#download-str-url-str-filename-int)
* [HTTPGet\( str url \) buf](network.md#httpget-str-url-buf)
* [HTTPPage\( str url \) str](network.md#httppage-str-url-str)

## Функции для работы с HTTP

### Download\( str url, str filename \) int

Функция _Download_ загружает файл из указанного URL и сохранаяет его с указанным именем. Функция возвращает размер загруженного файла.

```go
    str ftemp = TempDir() + `/readme.html`
    int size = Download("https://github.com/gentee/gentee", ftemp)
```

### HTTPGet\( str url \) buf

Функция _HTTPGet_ отправляет GET запрос по указанному URL и возвращает ответ в виде переменной типа _buf_. Функция может использоваться для загрузки небольших файлов без сохранения их на диск.

### HTTPPage\( str url \) str

Функция _HTTPPage_ отправляет GET запрос по указанному URL и возвращает ответ в виде строки.

