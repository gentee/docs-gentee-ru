# Криптография

Ниже описаны криптографические функции.

* [AESDecrypt\( str key, buf data \) buf](crypto.md#aesdecrypt-str-key-buf-data-buf)
* [AESEncrypt\( str key, buf data \) buf](crypto.md#aesencrypt-str-key-buf-data-buf)
* [Md5\( buf \| str data \) buf](crypto.md#md-5-buf-or-str-data-buf)
* [RandomBuf\( int size \) buf](crypto.md#randombuf-int-size-buf)
* [Sha256\( buf \| str data \) buf](crypto.md#sha-256-buf-or-str-data-buf)

## Функции

### AESDecrypt\( str key, buf data \) buf

Функция _AESDecrypt_ расшифровывает содержимое переменной типа *buf* с использованием ключа шифрования *key*. Зашифрованные данные должны быть получены с помощью функции *AESEncrypt*. Функция возвращает переменную типа *buf* с расшифрованными данными.

``` go
buf encrypted = AESDecrypt(`my password`, encrypted)
```

### AESEncrypt\( str key, buf data \) buf

Функция _AESEncrypt_ шифрует содержимое переменной типа *buf* используя алгоритм AES-256. Параметр *key* является ключом шифрования. Функция возвращает переменную типа *buf* с зашифрованными данными. Используйте функцию *AESDecrypt* для расшифровки данных.

``` go
buf crypted = AESEncrypt(`my password`, buf(`Test message`))
```

### Md5\(buf\|str data\) buf

Функция _Md5_ возвращает MD5 хэш переменной типа _buf_ или _str_.

### RandomBuf\(int size\) buf

Функция _RandomBuf_ возвращает переменную типа *buf*, которая содержит последовательность случайных байт указанного размера.

### Sha256\(buf\|str data\) buf

Функция _Sha256_ возвращает SHA256 хэш переменной типа _buf_ или _str_.
