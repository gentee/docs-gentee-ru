# Файлы

Ниже описаны функции для работы с файлами и директориями.

* [AppendFile\( str filename, buf \| str data \)](file.md#appendfile-str-filename-buf-str-data)
* [ChDir\( str dirname \)](file.md#chdir-str-dirname)
* [CopyFile\( str src, str dest \) int](file.md#copyfile-str-src-str-dest-int)
* [CreateDir\( str dirname \)](file.md#createdir-str-dirname)
* [FileInfo\( str name \) finfo](file.md#fileinfo-str-name-finfo)
* [GetCurDir\(\) str](file.md#getcurdir-str)
* [ReadDir\( str dirname \) arr.finfo](file.md#readdir-str-dirname-arrf-info)
* [ReadFile\( str filename \) str](file.md#readfile-str-filename-str)
* [ReadFile\( str filename, buf out \) buf](file.md#readfile-str-filename-buf-out-buf)
* [ReadFile\( str filename, int offset, int length \) buf](file.md#readfile-str-filename-int-offset-int-length-buf)
* [Remove\( str name \)](file.md#remove-str-name)
* [RemoveDir\( str dirname \)](file.md#removedir-str-dirname)
* [Rename\( str oldpath, str newpath \)](file.md#rename-str-oldpath-str-newpath)
* [SetFileTime\( str name, time modtime \)](file.md#setfiletime-str-name-time-modtime)
* [TempDir\(\) str](file.md#tempdir-str)
* [TempDir\( str path, str prefix \) str](file.md#tempdir-str-path-str-prefix-str)
* [WriteFile\( str filename, buf \| str data \)](file.md#writefile-str-filename-buf-str-data)

## Типы

### finfo

Тип _finfo_ используется для получения информации о файле и имеет следующие поля:

* **str Name** - имя файла
* **int Size** - размер файла в байтах
* **int Mode** - флаги файла и разрешения
* **time Time** - время последнего изменения
* **bool IsDir** - true, если это директория

## Functions

### AppendFile\(str filename, buf\|str data\)

Функция _AppendFile_ добавляет данные переменной типа _buf_ или _str_ в конец файла _filename_. Если файл не существует, то _AppendFile_ создает его с правами 0644.

### ChDir\(str dirname\)

Функция _ChDir_ изменяет текущую директорию.

### CopyFile\(str src, str dest\) int

Функция _CopyFile_ копирует файл _src_ в файл _dest_. Если файл _dest_ существует, то он будет перезаписан. Функция возвращает количество скопированных байт.

### CreateDir\(str dirname\)

Функция _CreateDir_ создает директорию с именем _dirname_, включая все необходимые родительские директории. Если _dirname_ уже существующая директория, то _CreateDir_ ничего не делает.

### FileInfo\(str name\) finfo

Функция _FileInfo_ получает информацию об указанном файле и возвращает структуру _finfo_.

### GetCurDir\(\) str

Функция _GetCurDir_ возвращает текущую директорию.

### ReadDir\(str dirname\) arr.finfo

Функция _ReadDir_ читает директорию с указанным именем и возвращает список её поддиректорий и файлов.

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

### TempDir\(\) str

Функция _TempDir_ возвращает временную директорию по умолчанию.

### TempDir\(str path, str prefix\) str

Функция _TempDir_ создает новую временную директорию в директории _path_ с именем, начинающемся на _prefix_ и возвращает полное имя этой новой директории. Если _path_ пустая строка, _TempDir_ использует временную директорию по умолчанию.

### WriteFile\(str filename, buf\|str data\)

Функция _WriteFile_ записывает данные из переменной типа _buf_ или строки в файл _filename_. Если файл не существует, то он будет создан с разрешениями 0777, в противном случае, файл будет перезаписан заново.

