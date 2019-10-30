# Массивы

Здесь описаны операторы и функции для работы с массивами **arr**. Запись **arr.typename** означает, что вы можете указать любой тип, но в случае бинарного оператора, этот тип должен быть одинаковым у обоих массивов.

* [Join\( arr.str a, str sep \) str](array.md#join-arr-str-a-str-sep-str)
* [Reverse\( arr.typename a \) arr.typename](array.md#reverse-arr-typename-a-arr-typename)
* [Slice\( arr.typename a, int start, int end \) arr.typename](array.md#slice-arr-typename-a-int-start-int-end-arr-typename)
* [Sort\( arr.str a \) arr.str](array.md#sort-arr-str-a-arr-str)

## Операторы

| Оператор | Результат | Описание |
| :--- | :--- | :--- |
| **\*** arr.typename | int | Возвращает количество элементов в массиве. |
| arr.typename **=** arr.typename | arr.typename | Присваивание. |
| arr.typename **&=** arr.typename | arr.typename | Создать клон массива. Новая переменная будет работать с тем же набором данных. |
| arr.typename **+=** arr.typename | arr.typename | Добавляет элементы из одного массива к другому. |
| arr.str **+=** str | arr.str | Добавление строки к массиву строк. |
| arr.int **+=** int | arr.int | Добавление целого числа к массиву чисел. |
| arr.bool **+=** bool | arr.bool | Добавление логического значения к массиву логических значений. |
| arr.arr.typename **+=** arr.typename | arr.arr.typename | Добавление массива к массиву массивов. |
| arr.map.typename **+=** map.typename | arr.map.typename | Добавление ассоциативного массива к массиву ассоциативных массивов. |
| arr.typename **\[** int **\]** | typename | Присвоить/получить значение массива по индексу. |

## Функции

### Join\(arr.str a, str sep\) str

Функция _Join_ объединяет строки массива в одну строку. Разделительная строка _sep_ вставляется между строками массива.

### Reverse\( arr.typename a \) arr.typename

Функция _Reverse_ меняет порядок элементов в массиве на противоположный и возвращает этот массив.

### Slice\( arr.typename a, int start, int end \) arr.typename

Функция _Slice_ создает новый массив с элементами от *start* (включая) до *end* (не включая). Функция возвращает созданный массив.

### Sort\( arr.str a \) arr.str

Функция _Sort_ сортирует переданный массив строк в порядке возрастания и возвращает его.

