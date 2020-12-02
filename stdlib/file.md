# Файлы

Ниже описаны функции для работы с файлами и директориями.

* [AppendFile\( str filename, buf \| str data \)](file.md#appendfile-str-filename-buf-or-str-data)
* [ChDir\( str dirname \)](file.md#chdir-str-dirname)
* [ChMode\( str name, int mode \)](file.md#chmode-str-name-int-mode)
* [CloseFile\( file f \)](file.md#closefile-file-f)
* [CopyFile\( str src, str dest \) int](file.md#copyfile-str-src-str-dest-int)
* [CreateDir\( str dirname \)](file.md#createdir-str-dirname)
* [CreateFile\( str name, bool trunc \)](file.md#createfile-str-name-bool-trunc)
* [ExistFile\( str name \) bool](file.md#existfile-str-name-bool)
* [FileInfo\( file f \) finfo](file.md#fileinfo-file-f-finfo)
* [FileInfo\( str name \) finfo](file.md#fileinfo-str-name-finfo)
* [FileMode\( str name \) int](file.md#filemode-str-name-int)
* [GetCurDir\(\) str](file.md#getcurdir-str)
* [IsEmptyDir\( str path \) bool](file.md#isemptydir-str-path-bool)
* [Md5File\( str filename \) str](file.md#md-5-file-str-filename-str)
* [obj\( finfo fi \) obj](file.md#obj-finfo-fi-obj)
* [OpenFile\( str filename, int flags \) file](file.md#openfile-str-filename-int-flags-file)
* [Read\( file f, int size \) buf](file.md#read-file-f-int-size-buf)
* [ReadDir\( str dirname \) arr.finfo](file.md#readdir-str-dirname-arr-finfo)
* [ReadDir\( str dirname, int flags, str pattern \) arr.finfo](file.md#readdir-str-dirname-int-flags-str-pattern-arr-finfo)
* [ReadDir\( str dirname, int flags, arr.str patterns, arr.str ignore \) arr.finfo](file.md#readdir-str-dirname-int-flags-arr-str-patterns-arr-str-ignore-arr-finfo)
* [ReadFile\( str filename \) str](file.md#readfile-str-filename-str)
* [ReadFile\( str filename, buf out \) buf](file.md#readfile-str-filename-buf-out-buf)
* [ReadFile\( str filename, int offset, int length \) buf](file.md#readfile-str-filename-int-offset-int-length-buf)
* [Remove\( str name \)](file.md#remove-str-name)
* [RemoveDir\( str dirname \)](file.md#removedir-str-dirname)
* [Rename\( str oldpath, str newpath \)](file.md#rename-str-oldpath-str-newpath)
* [SetFileTime\( str name, time modtime \)](file.md#setfiletime-str-name-time-modtime)
* [SetPos\( file f, int off, int whence \) int](file.md#setpos-file-f-int-off-int-whence-int)
* [Sha256File\( str filename \) str](file.md#sha-256-file-str-filename-str)
* [TempDir\(\) str](file.md#tempdir-str)
* [TempDir\( str path, str prefix \) str](file.md#tempdir-str-path-str-prefix-str)
* [Write\( file f, buf b \) file](file.md#write-file-f-buf-b-file)
* [WriteFile\( str filename, buf \| str data \)](file.md#writefile-str-filename-buf-or-str-data)

## Типы

### finfo

Тип _finfo_ используется для получения информации о файле и имеет следующие поля:

* **str Name** - имя файла
* **int Size** - размер файла в байтах
* **int Mode** - флаги файла и разрешения
* **time Time** - время последнего изменения
* **bool IsDir** - true, если это директория
* **str Dir** - директория, где расположен файл. Данное поле заполняется только при вызове функции [ReadDir(str, int, str)](file.md#readdir-str-dirname-int-flags-str-pattern-arr-finfo).

### file

Тип _file_ используется в функциях, которые работают с дескриптором открытого файла.

## Функции

### AppendFile\(str filename, buf\|str data\)

Функция _AppendFile_ добавляет данные переменной типа _buf_ или _str_ в конец файла _filename_. Если файл не существует, то _AppendFile_ создает его с правами 0644.

### ChDir\(str dirname\)

Функция _ChDir_ изменяет текущую директорию.

### ChMode\(str name, int mode\)

Функция _ChMode_ изменяет атрибуты файла.

### CloseFile\(file f\)

Функция _CloseFile_ закрывает дескриптор файла, который был открыт с помощью функции **OpenFile**.

### CopyFile\(str src, str dest\) int

Функция _CopyFile_ копирует файл _src_ в файл _dest_. Если файл _dest_ существует, то он будет перезаписан. При копировании сохраняются атрибуты файла. Функция возвращает количество скопированных байт.

### CreateDir\(str dirname\)

Функция _CreateDir_ создает директорию с именем _dirname_, включая все необходимые родительские директории. Если _dirname_ уже существующая директория, то _CreateDir_ ничего не делает.

### CreateFile\(str name, bool trunc\)

Функция _CreateFile_ создает файл с указанным именем. Если параметр _trunc_ равен _true_ и файл уже существует, то в этом случае его размер станет 0.

### ExistFile\(str name\) bool

Функция _ExistFile_ возвращает *true*, если указанный файл или директория существует. В противном случае, возвращается *false*.

### FileInfo\(file f\) finfo

Функция _FileInfo_ получает информацию об указанном файле и возвращает структуру _finfo_. Файл должен быть октрыт с помощью функции **OpenFile**.

### FileInfo\(str name\) finfo

Функция _FileInfo_ получает информацию об указанном файле и возвращает структуру _finfo_.

### FileMode\(str name\) int

Функция _FileMode_ возвращает атрибуты файла.

### GetCurDir\(\) str

Функция _GetCurDir_ возвращает текущую директорию.

### IsEmptyDir\(str path\) bool

Функция _IsEmptyDir_ возвращает _true_, если указанная директория пустая. В противном случае, возвращается _false_.

### Md5File\(str filename\) str

Функция _Md5File_ возвращает MD5 хэш указанного файла в виде шестнадцатеричной строки.

### obj\(finfo fi\) obj

Функция _obj_ конвертирует переменную типа finfo в объект. Полученный объект имеет поля: *name, size, mode, time, isdir, dir*.

### OpenFile\(str filename, int flags\) file

Функция _OpenFile_ открывает указанный файл и возвращает переменную типа _file_ с дескриптором открытого файла. После работы с файлом дескриптор открытого файла должен быть закрыт с помощью функции **CloseFile**. Параметр _flags_ может быть нулем или комбинацией следующих флагов:

* *CREATE* - если файл не существует, то он будет создан.
* *TRUNC* - файл будет обрезан до нулевой длины после открытия.
* *READONLY* - файл будет открыт только для чтения.

``` go
    file f = OpenFile(fname, CREATE)
    Write(f, buf("some test string"))
    SetPos(f, -15, 1)
    buf b &= Read(f, 5)
    CloseFile(f)
```

### Read\(file f, int size\) buf

Функция _Read_ читает _size_ количество байт с текущей позиции в файле, который был открыт с помощью функции **OpenFile**. Функция возвращает переменную типа _buf_, которая содержит прочитанные данные.

### ReadDir\(str dirname\) arr.finfo

Функция _ReadDir_ читает директорию с указанным именем и возвращает список её поддиректорий и файлов.

### ReadDir\(str dirname, int flags, str pattern\) arr.finfo

Функция _ReadDir_ читает директорию *dirname* с указанным именем и возвращает список её поддиректорий и файлов в соотвествии с указанными параметрами. Параметр *flags* может быть комбинацией следующих флагов:

* **RECURSIVE** - В этом случае будет рекурсивный поиск по всем поддиректориям.
* **ONLYFILES** - Возвращаемый массив будет содержать только файлы.
* **ONLYDIRS** - Возвращаемый массив будет содержать только директории.
* **REGEXP** - Параметр *pattern* содержит регулярное выражения для сравнения имён файлов.

Если вы укажете одновременно флаги **ONLYFILES** и **ONLYDIRS**, то будут искаться файлы и директории.

Параметр *pattern* может содержать маску для файлов или регулярное выражение. В этом случае, будут возвращаться файлы и директории, которые соответствуют указанному шаблону. Маска может содержать следующие символы:

* '\*' - любая последовательность, кроме символа разделителя
* '?' - любой одиночный символ, кроме символа разделителя

``` go
for item in ReadDir(ftemp, RECURSIVE, `*fold*`) {
    ret += item.Name
}
for item in ReadDir(ftemp, RECURSIVE | ONLYFILES | REGEXP, `.*\.pdf`) {
    ret += item.Name
}
```

### ReadDir\(str dirname, int flags, arr.str patterns, arr.str ignore\) arr.finfo

Функция _ReadDir_ читает директорию *dirname* с указанным именем и возвращает список её поддиректорий и файлов в соотвествии с указанными параметрами. Параметр *flags* описан выше. Параметр *patterns* является массивом строк и может содержать маски для файлов или регулярные выражения. Параметр *ignore* также содержит маски для файлов или регулярные выражения, но такие файлы или директории будут пропускаться. Если вы хотите указать в этих массивах регулярное выражение, то заключите его между символами **'/'**.

``` go
arr.str aignore = {`/txt/`, `*.pak`}
arr.str amatch = {`/\d+/`, `*.p??`, `/di/`}
for item in ReadDir(ftemp, RECURSIVE, amatch, aignore) {
    ret += item.Name
}
```

### ReadFile\(str filename\) str

Функция _ReadFile_ читает указанный файл и возвращает его содержимое в виде строки.

### ReadFile\(str filename, buf out\) buf

Функция _ReadFile_ читает файл _filename_ в переменную _out_ типа _buf_ и возвращает эту переменную.

### ReadFile\(str filename, int offset, int length\) buf

Функция _ReadFile_ читает данные из файла _filename_ начиная со смещения _offset_ и длиной _length_. Если _offset_ меньше нуля, то смещение считается от конца к началу файла.

### Remove\(str name\)

Функция _Remove_ удаляет файл или пустую директорию.

### RemoveDir\(str dirname\)

Функция _RemoveDir_ удаляет директорию _dirname_ включая всё её содержимое.

### Rename\(str oldpath, str newpath\)

Функция _Rename_ переименовывает \(переносит\) _oldpath_ в _newpath_. Если _newpath_ уже существует и является файлом, то _Rename_ заменяет его.

### SetFileTime\(str name, time modtime\)

Функция _SetFileTime_ изменяет время последней записи у указанного файла.

### SetPos\(file f, int off, int whence\) int

Функция _SetPos_ устанавливает в файле текущую позицию для операций чтения или записи. Файл должен быть открыт с помощью функции **OpenFile**. Функция возвращает смещение новой позиции. Параметр _whence_ может принимать следующие значения:

* *0* - смещение _off_ указано от начало файла.
* *1* - смещение _off_ указано от текущей позиции.
* *2* - смещение _off_ указано от конца файла.

### Sha256File\(str filename\) str

Функция _Sha256File_ возвращает SHA256 хэш указанного файла в виде шестнадцатеричной строки.

### TempDir\(\) str

Функция _TempDir_ возвращает временную директорию по умолчанию.

### TempDir\(str path, str prefix\) str

Функция _TempDir_ создает новую временную директорию в директории _path_ с именем, начинающемся на _prefix_ и возвращает полное имя этой новой директории. Если _path_ пустая строка, _TempDir_ использует временную директорию по умолчанию.

### Write\(file f, buf b\) file

Функция _Write_ записывает данные из переменной типа _buf_ в файл, который был открыт с помощью функции **OpenFile**. Функция возвращает параметр _f_.

### WriteFile\(str filename, buf\|str data\)

Функция _WriteFile_ записывает данные из переменной типа _buf_ или строки в файл _filename_. Если файл не существует, то он будет создан с разрешениями 0777, в противном случае, файл будет перезаписан заново.
