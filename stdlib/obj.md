# Объект

Тип **obj** служит для хранения значений следующих типов - **int, bool, float, str, arr.obj, map.obj**. Если объекту не присвоено никакое значение, то он равен **nil**. Объекту можно присваивать значения  типа, который отличается от текущего.  
Здесь описаны операторы и функции для работы с объектами.

* [arr\( obj o \) arr.obj](obj.md#arr-obj-o-arr-obj)
* [bool\( obj o \) bool](obj.md#bool-obj-o-bool)
* [bool\( obj o, bool def \) bool](obj.md#bool-obj-o-bool-def-bool)
* [float\( obj o \) float](obj.md#float-obj-o-float)
* [float\( obj o, float def \) float](obj.md#float-obj-o-float-def-float)
* [int\( obj o \) int](obj.md#int-obj-o-int)
* [int\( obj o, int def \) int](obj.md#int-obj-o-int-def-int)
* [IsNil\( obj o \) bool](obj.md#isnil-obj-o-bool)
* [item\( obj o, int i \) obj](obj.md#item-obj-o-int-i-obj)
* [item\( obj o, str s \) obj](obj.md#item-obj-o-str-s-obj)
* [map\( obj o \) map.obj](obj.md#map-obj-o-map-obj)
* [obj\( arr.typename a \) obj](obj.md#obj-arr-typename-a-obj)
* [obj\( bool b \) obj](obj.md#obj-bool-b-obj)
* [obj\( float f \) obj](obj.md#obj-float-f-obj)
* [obj\( int i \) obj](obj.md#obj-int-i-obj)
* [obj\( map.typename m \) obj](obj.md#obj-map-typename-m-obj)
* [obj\( str s \) obj](obj.md#obj-str-s-obj)
* [Sort\( arr.obj o, cmpobjfunc cmpfunc \) arr.obj](obj.md#sort-arr-obj-o-cmpobjfunc-cmpfunc-arr-obj)
* [str\( obj o \) str](obj.md#str-obj-o-str)
* [str\( obj o, str def \) str](obj.md#str-obj-o-str-def-str)
* [Type\( obj o \) str](obj.md#type-obj-o-str)

## Типы

### fn cmpobjfunc(obj, obj) int

Тип функций **cmpobjtype** служит для сравнения двух объектов. Функции этого типа используются для сортировки объектов в массиве.

## Операторы

| Оператор | Результат | Описание |
| :--- | :--- | :--- |
| *obj | int | Если объект является _arr.obj_ или _map.obj_, то возвращается количество элементов в массиве. В противном случае, возвращается 0. |
| obj **?** | bool | Вызов *bool(obj)*. |
| obj **=** arr.typename | obj | Присваивание массива объекту. |
| obj **=** bool | obj | Присваивание логического значения объекту. |
| obj **=** float | obj | Присваивание десятичного числа объекту. |
| obj **=** int | obj | Присваивание числа объекту. |
| obj **=** map.typename | obj | Присваивание ассоциативного массива объекту. |
| obj **=** obj | obj | Присваивание объектов. |
| obj **=** str | obj | Присваивание строки объекту. |
| obj **+=** obj | obj | Добавление объекта к массиву объектов. |
| obj **&=** obj | obj | Создать клон объекта. Новая переменная будет работать с тем же набором данных. |
| obj **\[** int/str **\]** | obj | Присвоить/получить значение массива по индексу. Если объект не является _arr.obj_ или _map.obj_, то возвращается ошибка. |

## Функции

### arr\(obj o\) arr.obj

Функция _arr_ возвращает массив объектов. Объект _o_ должен быть массивом, в противном случае возвращается ошибка. При вызове функции не создается нового массива, а возвращается текущий массив, который содержит объект _o_.

### bool\(obj o\) bool

Функция _bool_ возвращает логическое значение текущего типа. Например, если объект содержит строку, то возвращается результат вызова _bool(str)_. Если объект не определен, то возвращается ошибка.

### bool\(obj o, bool def\) bool

Функция _bool_ возвращает логическое значение текущего типа. Если объект не определен, то возвращается второй параметр.

### float\(obj o\) float

Функция _float_ конвертирует объект в действительное число. Объект должен содержать значение типа **str, int, float**, в противном случае, возвращается ошибка.

### float\(obj o, float def\) float

Функция _float_ конвертирует объект в действительное число. Если объект не определен, то возвращается второй параметр.

### int\(obj o\) int

Функция _int_ конвертирует объект в целое число. Объект должен содержать значение типа **str, int, float, bool**, в противном случае, возвращается ошибка.

### int\(obj o, int def\) int

Функция _int_ конвертирует объект в целое число. Если объект не определен, то возвращается второй параметр.

### IsNil\(obj o\) bool

Функция _IsNil_ возвращает _true_, если объект не определен (равен **nil**). В противном случае, функция возвращает _false_.

### item\(obj o, int i\) obj

Функция _item_ возвращает i-й элемент объекта. Объект должен иметь тип **arr.obj**. Если элемент отсутствует, то возвращается пустой объект.

### item\(obj o, str s\) obj

Функция _item_ возвращает значение ключа **s**. Объект должен иметь тип **map.obj**. Если элемент отсутствует, то возвращается пустой объект.

### map\(obj o\) map.obj

Функция _map_ возвращает ассоциативный массив объектов. Объект _o_ должен быть ассоциативным массивом (map), в противном случае возвращается ошибка. При вызове функции не создается нового массива, а возвращается текущий *map*, который содержит объект _o_.

### obj\(arr.typename a\) obj

Функция _obj_ конвертирует массив типа _arr_ в объект.

### obj\(bool b\) obj

Функция _obj_ создает объект с указанными логическим значением.

### obj\(float f\) obj

Функция _obj_ создает объект с указанными **float** значением.

### obj\(int i\) obj

Функция _obj_ создает объект с указанными **int** значением.

### obj\(map.typename m\) obj

Функция _obj_ конвертирует ассоциативный массив типа _map_ в объект.

### obj\(str s\) obj

Функция _obj_ создает объект с указанными **str** значением.

### Sort\(arr.obj o, cmpobjfunc cmpfunc\) arr.obj

Функция _Sort_ сортирует массив объектов и возвращает его. Сортировка происходит с помощью функции типа **cmpobjfunc**.

``` go
func mySort(obj left, obj right) int {
  if str(left) < str(right) : return -1
  if str(left) > str(right) : return 1
  return 0
}

run str {
  arr a = {"qwr","7","10","ab","тест","абв", "ka"}
  obj o = a
  Sort( arr(o), &mySort.cmpobjfunc )
  ...
}
```

### str\(obj o\) str

Функция _str_ преобразует объект в строку и возвращает её.

### str\(obj o, str def\) str

Функция _str_ преобразует объект в строку и возвращает её. Если объект не определен, то возвращается второй параметр.

### Type\(obj o\) str

Функция _Type_ возвращает тип значения указанного объекта. Могут возвращаться следующие типы: **int, bool, float, str, arr.obj, map.obj**. Если объект не определен, то возвращается **nil**.
