# Сеть

Здесь описаны функции для работы с сетью/интернетом.

* [Download\( str url, str filename \) int](network.md#download-str-url-str-filename-int)
* [HTTPGet\( str url \) buf](network.md#httpget-str-url-buf)
* [HTTPPage\( str url \) str](network.md#httppage-str-url-str)
* [HTTPRequest\( str url, str method, map.str params, map.str headers \) str](network.md#httprequest-str-url-str-method-map-str-headers-str)

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

### HTTPRequest\( str url, str method, map.str params, map.str headers \) str

Функция _HTTPRequest_ отправляет HTTP запрос по указанному URL и возвращает ответ в виде строки. В параметре _method_ необходимо указать метод вызова - **GET, POST, UPDATE, PUT, DELETE*. Также функция позволяет указывать параметры и заголовки запроса, они описываются в виде ассоциативных массивов, где в качестве ключа указано имя параметра или имя заголовка. По умолчанию, при вызове *POST* параметры передаются как данные формы. Если вы хотите передавать их в JSON формате, то параметре *headers* укажите *"Content-Type": "application/json; charset=UTF-8"*.

``` go
    map empty
    Println(HTTPRequest(TESTURL, "GET", empty, empty))
    map params = { `name`: `Jong Doe`, `id`: `101` }
    Println(HTTPRequest(TESTURL, "GET", params, empty))
    Println(HTTPRequest(TESTURL, "POST", params, empty))
    map headjson = { `Content-Type`: `application/json; charset=UTF-8` }
    Println(HTTPRequest(TESTURL, "POST", params, headjson))
```
