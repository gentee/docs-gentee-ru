# Архивация

Здесь описаны функции для работы с архивами **zip** и **tar.gz**.

* [ArchiveName\( finfo fi, str root \) str](archive.md#archivename-finfo-fi-str-root-str)
* [CloseTarGz\( handle h \)](archive.md#closetargz-handle-h)
* [CloseZip\( handle h \)](archive.md#closezip-handle-h)
* [CreateTarGz\( str name \) handle](archive.md#createtargz-str-name-handle)
* [CreateZip\( str name \) handle](archive.md#createzip-str-name-handle)
* [CompressFile\( handle h, str fname, str packname \)](archive.md#compressfile-handle-h-str-fname-str-packname)
* [ReadTarGz\( str name \) arr.finfo](archive.md#readtargz-str-name-arr-finfo)
* [ReadZip\( str name \) arr.finfo](archive.md#readzip-str-name-arr-finfo)
* [TarGz\( str name, str path \)](archive.md#targz-str-name-str-path)
* [UnpackTarGz\( str name, str path \)](archive.md#unpacktargz-str-name-str-path)
* [UnpackTarGz\( str name, str path, arr pattern, arr ignore \)](archive.md#unpacktargz-str-name-str-path-arr-pattern-arr-ignore)
* [UnpackZip\( str name, str path \)](archive.md#unpackzip-str-name-str-path)
* [UnpackZip\( str name, str path, arr pattern, arr ignore \)](archive.md#unpackzip-str-name-str-path-arr-pattern-arr-ignore)
* [Zip\( str name, str path \)](archive.md#zip-str-name-str-path)

## Функции

### ArchiveName\(finfo fi, str root\) str

Функция _ArchiveName_ объединяет поля *Name* и *Dir* в переменной типа *finfo* и возвращает путь файла для архива  относительно корневого пути *root*.

### CloseTarGz\(handle h\)

Функция _CloseTarGz_ заканчивает создание *.tar.gz* архива. Параметр _h_ - это идентификатор, который был возвращен функцией **CreateTarGz**.

### CloseZip\(handle h\)

Функция _CloseZip_ заканчивает создание *.zip* архива. Параметр _h_ - это идентификатор, который был возвращен функцией **CreateZip**.

### CreateTarGz\(str name\) handle

Функция _CreateTarGz_ начинает создание **.tar.gz** архива с указанным именем. Вы можете добавлять файлы в этот архив с помощью функции **CompressFile**. Функция возвращает идентификатор, который нужно будет закрыть с помощью функции _CloseTarGz_.

### CreateZip\(str name\) handle

Функция _CreateZip_ начинает создание **.zip** архива с указанным именем. Вы можете добавлять файлы в этот архив с помощью функции **CompressFile**. Функция возвращает идентификатор, который нужно будет закрыть с помощью функции _CloseZip_.

### CompressFile\(handle h, str fname, str packname\)

Функция _CompressFile_ добавляет указанный файл _fname_ в создаваемый архив. Параметр _packname_ содержит относительный путь и имя файла с которым он будет сохранен в архиве. В качестве разделителя нужно использовать символ **/**. Архив предварительно должен быть создан с помощью функций **CreateZip** или **CreateTarGz**.

``` go
    handle zip = CreateZip(`my.zip`)
    CompressFile(zip, `../data/my.txt`, `my.txt`)
    CompressFile(zip, `/home/user/folder/copy.txt`, `folder/copy.txt`)
    CloseZip(zip)
```

### ReadTarGz\(str name\) arr.finfo

Функция _ReadTarGz_ возвращает список файлов в указанном **tar.gz** архиве. Поле *Name* содержит имя файла вместе с относительным путем.

``` go
   arr.finfo list = ReadTarGz(`my.tar.gz`)
   for fi in list : Println( "\{fi.Name} \{fi.Size}")
```

### ReadZip\(str name\) arr.finfo

Функция _ReadZip_ возвращает список файлов в указанном **zip** архиве. Поле *Name* содержит имя файла вместе с относительным путем.

### TarGz\(str name, str path\)

Функция _TarGz_ упаковывает файл или содержимое директории _path_ в **.tar.gz** архив с именем _name_.

``` go
   TarGz("/home/user/out/my.tar.gz", `/home/user/docs`)
```

### UnpackTarGz\(str name, str path\)

Функция _UnpackTarGz_ распаковывает **.tar.gz** архив с именем _name_ в директорию _path_.

``` go
   UnpackTarGz("/home/user/out/my.tar.gz", `/home/user/olddocs`)
```

### UnpackTarGz\(str name, str path, arr pattern, arr ignore\)

Функция _UnpackTarGz_ выборочно распаковывает **.tar.gz** архив с именем _name_ в директорию _path_. Массив _pattern_ содержит шаблоны файлов, которые необходимо распаковать. Массив _ignore_ содержит шаблоны файлов, которые необходимо пропустить. Параметры _pattern_ и _ignore_ могу быть пустыми массивами. Если шаблон начинается и заканчивается символом **/**, то он обрабатывается как регулярное выражение.

``` go
   arr empty
   arr doc = {`*.docx`, `/.txt$/`}
   UnpackTarGz("/home/user/out/my.tar.gz", `/home/user/tmp`, doc, empty )
```

### UnpackZip\(str name, str path\)

Функция _UnpackZip_ распаковывает **.zip** архив с именем _name_ в директорию _path_.

``` go
   UnpackZip("/home/user/out/my.zip", `/home/user/olddocs`)
```

### UnpackZip\(str name, str path, arr pattern, arr ignore\)

Функция _UnpackZip_ выборочно распаковывает **.zip** архив с именем _name_ в директорию _path_. Массив _pattern_ содержит шаблоны файлов, которые необходимо распаковать. Массив _ignore_ содержит шаблоны файлов, которые необходимо пропустить. Параметры _pattern_ и _ignore_ могу быть пустыми массивами. Если шаблон начинается и заканчивается символом **/**, то он обрабатывается как регулярное выражение.

``` go
   arr empty
   arr skip = {`/temp.pdf/`, `/.txt$/`}
   UnpackZip("/home/user/out/my.tar.gz", `/home/user/tmp`, empty, skip )
```

### Zip\(str name, str path\)

Функция _Zip_ упаковывает файл или содержимое директории _path_ в **.zip** архив с именем _name_.

``` go
   Zip("/home/user/out/mydoc.zip", `/home/user/docs/important.docx`)
```
