# Ассоциативные массивы

Здесь описаны операторы и функции для работы с ассоциативными массивами **map**. Запись **map.typename** означает, что вы можете указать любой тип, но в случае бинарного оператора, этот тип должен быть одинаковым у обоих массивов.

* [bool\( map.typename m \) bool](map.md#bool-map-typename-m-bool)
* [Del\( map.typename m, str key \) map.typename](map.md#del-map-typename-m-str-key-map-typename)
* [IsKey\( map.typename m, str key \) bool](map.md#iskey-map-typename-m-str-key-bool)
* [Key\( map.typename m, int index \) str](map.md#key-map-typename-m-int-index-str)

## Операторы

| Оператор | Результат | Описание |
| :--- | :--- | :--- |
| **\*** map.typename | int | Возвращает количество элементов в массиве. |
| map.typename **?** | bool | Вызов *bool(map.typename)*. |
| map.typename **=** map.typename | map.typename | Присваивание. |
| map.typename **&=** map.typename | map.typename | Создать клон ассоциативного массива. Новая переменная будет работать с тем же набором данных. |
| map.typename **\[** str **\]** | typename | Присвоить/получить значение ассоциативного массива по ключу. |

## Функции

### bool\(map.typename m\) bool

Функция _bool_ возвращает _false_, если ассоциативный массив пустой. В противном случае, возвращается _true_.

### Del\( map.typename m, str key \) map.typename

Функция _Del_ удалять указанный ключ и его значение из массива _map_. Возвращается параметр _m_.

### IsKey\( map.typename m, str key \) bool

Функция _IsKey_ возвращает _true_, если в ассоциативном массиве _m_ существует значение с указанным ключом и _false_, в противном случае.

### Key\( map.typename m, int index \) str

Функция _Key_ возвращает ключ элемента по его индексу. Например, эта функция может быть использована  в цикле *for* для получения ключа элемента.

``` go 
for val,i in mymap {
    Println("\(Key(mymap, i)):\(val)")
}
```
