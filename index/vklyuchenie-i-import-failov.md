# Включение и импорт файлов

### Включение и импорт файлов

Описание **include** импортирует все типы, функции и константы из указанных файлов и их дочерних файлов включенных с помощью **include**.

Описание **import** импортирует только публичные типы, функции и константы из указанных файлов и их дочерних файлов включенных с помощью **include**. Публичные объекты определяются с помощью ключевого слова **pub**.

```text
stringConst         = "`" { unicode_char } "`" | stringDoubleConst
stringDoubleConst = `"` { unicode_char | uShort | uLong | escapedChar | byteVal } `"`
importDecl = "import" "{" {stringConst newline} "}"
includeDecl = "include" "{" {stringConst newline} "}"
```

Рассмотрим видимость объектов в виде таблицы. Пусть имеется два файла.

```text
// a.g can include or import b.g
func afunc(i int) : return i*2
pub func apubfunc(i int) : return i*3

// b.g 
func bfunc(i int) : return i*4
pub func bpubfunc(i int) : return i*5
```

Пусть файл _c.g_ может импортировать или включать файл _a.g_. Вы можете видеть какие функции будут видимы в файле _c.g_ в зависимости от различных ситуаций.

|  | include a   a includes b | include a   a imports b | import a   a includes b | import a   a imports b |
| :--- | :--- | :--- | :--- | :--- |
| afunc | visible | visible |  |  |
| apubfunc | visible | visible | visible | visible |
| bfunc | visible |  |  |  |
| bpubfunc | visible |  | visible |  |

### Описание pub

Команда **pub** определяет следующую функцию, тип или константы как публичные. Вы можете импортировать их с помощью команды **import**.

```text
pubDecl = "pub" [newline]
objects = [pubDecl] (structDecl | FnDecl | ConstDecl | FunctionDecl)
```

Ключевое слово **pub** указывает, что следующая функция, константы или тип будут передаваться в случае импорта файла.

```text
pub const IOTA {  // public constants. Visible when include or import
    MY1
    MY2
}

const IOTA*2 {  // private constants. Visible only when include
    MY3
    MY4
}
```

