# Конвертация

Здесь описаны функции для конвертации данных из одного представления в другое.

* [Json\( obj o \) str](encoding.md#json-obj-o-str)
* [JsonToObj\( str s \) obj](encoding.md#jsontoobj-str-s-obj)
* [StructDecode\( b buf, struct s \)](encoding.md#structdecode-buf-b-struct-s)
* [StructEncode\( struct s \) buf](encoding.md#structencode-struct-s-buf)

## Функции

### Json\( obj o \) str

Функция _Json_ преобразует переменную типа *_obj_* в **json** строку.

### JsonToObj\( str s \) obj

Функция _JsonToObj_ преобразует **json** строку в переменную типа *_obj_*.


``` go 
run str {
  return Json(JsonToObj(`{
         "int": 1234,
         "str": "value",
         "float": -45.67,
          "list":[{"on": true},
            "sub 2",
            "sub 3",
            {
                "q": "OK"
            }]
    }`))
}
// Result {"float":-45.67,"int":1234,"list":[{"on":true},"sub 2","sub 3",{"q":"OK"}],"str":"value"}
```

### StructDecode\( buf b, struct s \)

Функция _StructDecode_ преобразует двоичные данные переменной типа *buf* в значения полей указанной структурной переменной. Двоичные данные должны быть созданы функцией *StructEncode*.

``` go
  time t
  StructDecode(StructEncode(Now()), t)
```

### StructEncode\( struct s \) buf

Функция _StructEncode_ преобразует переменную структурного типа в двоичный вид и сохраняет результат в переменную типа *buf*. Сохраняются только поля типа: **int,bool,char,float,buf,str**. Поля остальных типов пропускаются.

``` go
struct tmp {
    str head
    int i
}

run str {
  tmp t1 = {head: `HEADER`, i: -356}
  buf bout = StructEncode(t1)
  ...
}
```
