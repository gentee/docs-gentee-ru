# Конвертация

Здесь описаны функции для конвертации данных из одного представления в другое.

* [Json\( obj o \) str](encoding.md#json-obj-o-str)
* [JsonToObj\( str s \) obj](encoding.md#jsontoobj-str-s-obj)

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
