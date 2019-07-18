# Ассоциативные массивы

Здесь описаны операторы и функции для работы с ассоциативными массивами **map**. Запись **map.typename** означает, что вы можете указать любой тип, но в случае бинарного оператора, этот тип должен быть одинаковым у обоих массивов.

* [Del\( map.typename m, str key \) map.typename](map.md#del-map-typename-m-str-key-map-typename)
* [IsKey\( map.typename m, str key \) bool](map.md#iskey-map-typename-m-str-key-bool)

## Операторы

| Оператор | Результат | Описание |
| :--- | :--- | :--- |
| **\*** map.typename | int | Возвращает количество элементов в массиве. |
| map.typename **=** map.typename | map.typename | Присваивание. |
| map.typename **&=** map.typename | map.typename | Создать клон ассоциативного массива. Новая переменная будет работать с тем же набором данных. |
| map.typename **\[** str **\]** | typename | Присвоить/получить значение ассоциативного массива по ключу. |

## Функции

### Del\( map.typename m, str key \) map.typename

Функция _Del_ удалять указанный ключ и его значение из массива _map_. Возвращается параметр _m_.

### IsKey\( map.typename m, str key \) bool

Функция _IsKey_ возвращает _true_, если в ассоциативном массиве _m_ существует значение с указанным ключом и _false_, в противном случае.
