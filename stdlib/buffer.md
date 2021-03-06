# Буфер

Здесь описаны операторы и функции для работы со двоичными данными в виде массива байт \(тип **buf**\).

* [bool\( buf b \) bool](buffer.md#bool-buf-b-bool)
* [buf\( str s \) buf](buffer.md#buf-str-s-buf)
* [str\( buf b \) str](buffer.md#str-buf-b-str)
* [Base64\( buf b \) str](buffer.md#base-64-buf-b-str)
* [DecodeInt\( buf b, int offset \) int](buffer.md#decodeint-buf-b-int-offset-int)
* [Del\( buf b, int off, int length \) buf](buffer.md#del-buf-b-int-off-int-length-buf)
* [EncodeInt\( buf b, int i \) buf](buffer.md#encodeint-buf-b-int-i-buf)
* [Hex\( buf b \) str](buffer.md#hex-buf-b-str)
* [Insert\( buf b, int off, buf src\) buf](buffer.md#insert-buf-b-int-off-buf-src-buf)
* [SetLen\( buf b, int size \) buf](buffer.md#setlen-buf-b-int-size-buf)
* [Subbuf\( buf b, int off, int length \) buf](buffer.md#subbuf-buf-b-int-off-int-length-buf)
* [UnBase64\( str s \) buf](buffer.md#unbase-64-str-s-buf)
* [UnHex\( str s \) buf](buffer.md#unhex-str-s-buf)
* [Write\( buf b, int off, buf src \) buf](buffer.md#write-buf-b-int-off-buf-src-buf)

## Операторы

| Оператор | Результат | Описание |
| :--- | :--- | :--- |
| **\*** buf | int | Получить размер буфера в байтах. |
| buf **?** | bool | Вызов *bool(buf)*. |
| buf **+** buf | buf | Объединить два буфера. |
| buf **=** buf | buf | Присваивание двоичных данных. |
| buf **&=** buf | buf | Создать клон буфера. Новая переменная будет работать с тем же набором данных. |
| buf **+=** buf | buf | Добавить один буфер к другому. |
| buf **+=** int | buf | Добавить один байт к буферу. Число должно быть меньше 256. |
| buf **+=** str | buf | Добавить строку к буферу. |
| buf **+=** char | buf | Добавить символ к буферу. |
| buf **\[** int **\]** | int | Присвоить/получить байт по индексу. |

## Функции

### bool\(buf b\) bool

Функция _bool_ возвращает _false_, если буфер пустой. В противном случае, возвращается _true_.

### buf\(str s\) buf

Функция _buf_ конвертирует строку в значение типа _buf_ и возвращает его.

### str\(buf b\) str

Функция _str_ конвертирует значение типа _buf_ в строку и возвращает её.

### Base64\(buf b\) str

Функция _Base64_ преобразует значение типа _buf_ в строку в кодировке **base64** и возвращает её.

### DecodeInt\(buf b, int offset\) int

Функция _DecodeInt_ получает целое число из параметра типа _buf_. _offset_ - смещение в буфере, по которому необходимо прочитать число. Функция читает 8 байт и возвращает их как целое число.

### Del\(buf b, int off, int length\) buf

Функция _Del_ удалять часть данных из массива байт. _off_ - смещение удаляемых данных, _length_ - количество удаляемых байт. Если _length_ меньше нуля, то данные будут удаляться слева от указанного смещения. Функция возвращает переменную _b_, в которой произошло удаление.

### EncodeInt\(buf b, int i\) buf

Функция _EncodeInt_ добавляет целое число к указанной переменной типа _buf_. Так как значение *int* занимает 8 байт, то к буферу добавляется 8 байт независимо от значения параметра _i_. Функция возвращает параметр *b*.

### Hex\(buf b\) str

Функция _Hex_ преобразует значение типа _buf_ в шестнадцатеричную строку и возвращает её.

### Insert\(buf b, int off, buf src\) buf

Функция _Insert_ вставляет массив байт _src_ в массив _b_. _off_ - смещение, куда будет вставлен указанный массив байт. Функция возвращает переменную _b_.

### SetLen\(buf b, int size\) buf

Функция _SetLen_ устанавливает размер буфера. Если _size_ меньше размера буфера, то он будет обрезан. В противном случае, буфер будет дополнен нулями до указанного размера.

### Subbuf\(buf b, int off, int length\) buf

Функция _Subbuf_ возвращает возвращает новый буфер, который содержит фрагмент буфера _b_ с указанным смещением и длиной.

### UnBase64\(str s\) buf

Функция _UnBase64_ преобразует строку в кодировке **base64** в значение типа _buf_ и возвращает его.

### UnHex\(str s\) buf

Функция _UnHex_ преобразует шестнадцатеричную строку в значение типа _buf_ и возвращает его. Входящая строка должна содержать только шестнадцатеричные символы.

### Write\(buf b, int off, buf src\) buf

Функция _Write_ записывает массив байт переменной _src_ в переменную _b_ начиная с указанного смещения. Данные записываются поверх существующих значений. Функция возвращает переменную _b_.
