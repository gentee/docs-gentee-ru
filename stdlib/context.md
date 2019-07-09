---
nav: tocru
---

# Контекст

В языке Gentee отсутствуют глобальные переменные. Одним из способов обмена данными является специальный ассоциативный массив строк. Любая функция может безопасно добавлять туда пары ключ-значение или получать значение по ключу. Кроме этого, в контекст встроена возможность подстановки других существующих значений из контекста. Например, если определены пары _"a": "String A"_ и _"b": "String B"_, то _"\#a\# and \#b\#"_ возвратит _"String A and String B"_. Ниже описаны функции и операторы для работы с контекстом.

* [Ctx\( str input \) str](context.md#ctxstr-input-str)
* [CtxGet\( str key \) str](context.md#ctxgetstr-key-str)
* [CtxIs\( str key \) bool](context.md#ctxisstr-key-bool)
* [CtxSet\( str key, str val \) str](context.md#ctxsetstr-key-str-val-str)
* [CtxSet\( str key, bool b \) str](context.md#ctxsetstr-key-bool-b-str)
* [CtxSet\( str key, float f \) str](context.md#ctxsetstr-key-float-f-str)
* [CtxSet\( str key, int i \) str](context.md#ctxsetstr-key-int-i-str)
* [CtxValue\( str key \) str](context.md#ctxvaluestr-key-str)

## Операторы

| Оператор | Результат | Описание |
| :--- | :--- | :--- |
| **\#** ident | str | Тоже самое, что _CtxGet\(key\)_, где _ident_ является ключом контекста. |
| **\#\#** str | str | Тоже самое, что _Ctx\(str\)_. Указывается любое выражение, которое возвращает строку. |
| ident **\#=** str | str | Тоже самое, что _CtxSet\(str key, str s\)_, где _ident_ - это ключ контекста. |
| ident **\#=** bool | str | Тоже самое, что _CtxSet\(str key, bool b\)_, где _ident_ - это ключ контекста. |
| ident **\#=** float | str | Тоже самое, что _CtxSet\(str key, float f\)_, где _ident_ - это ключ контекста. |
| ident **\#=** int | str | Тоже самое, что _CtxSet\(str key, int i\)_, где _ident_ - это ключ контекста. |

```text
run str {
  str s = ` #AºB#`
  AºB #= `ººº`
  b #= 71
  CD #= `#AºB# #b# == ` 
  return #CD + #b + ##s
}
// ººº 71 == 71 ººº
```

## Функции

### Ctx\(str input\) str

Функция _Ctx_ заменяет в строке _input_ подстроки **\#keyname\#** на значение соответствующего ключа, если он существует.

```text
run str {
    CtxSetBool(`qq`, true)
    CtxSetFloat(`ff`, 3.1415)
    CtxSet(`out`, "it is #qq# that PI equals #ff#")
    return Ctx("#out#. #notexist#")
}
// it is true that PI equals 3.1415. #notexist#
```

### CtxGet\(str key\) str

Функция _CtxGet_ получает значение ключа _key_, заменяет в нём все вхождения других ключей и возвращает полученную строку. Если указанный ключ отсутствует, то возвратится пустая строка.

```text
func init {
   CtxSet(`a1`, `end`)
   CtxSet(`a2`, `=#a1#=`)
   CtxSet(`a3`, `+#a2#+#a1#`)
}

run str {
    init()
    return CtxGet(`a3`)
}
// +=end=+end
```

### CtxIs\(str key\) bool

Функция _CtxIs_ возвращает _true_, если в контексте существует значение с указанным ключом. В противном случае, возвращается _false_.

### CtxSet\(str key, str val\) str

Функция _CtxSet_ добавляет ключ и значение в контекст. Если ключ уже существует, то ему будет присвоено новое значение. Функция возвращает присвоенное значение ключа.

### CtxSet\(str key, bool b\) str

Функция _CtxSet_ добавляет ключ и логическое значение _b_ в контекст. Логическое значение будет преобразовано к строке _true_ или _false_. Функция возвращает присвоенное значение ключа.

### CtxSet\(str key, float f\) str

Функция _CtxSet_ добавляет ключ и число с плавающей точкой _f_ в контекст. Число будет преобразовано в строку. Функция возвращает присвоенное значение ключа.

### CtxSet\(str key, int i\) str

Функция _CtxSet_ добавляет ключ и целое число _i_ в контекст. Число будет преобразовано в строку. Функция возвращает присвоенное значение ключа.

### CtxValue\(str key\) str

Функция _CtxValue_ возвращает значение ключа _key_ как есть. В отличие от функции **CtxGet**, она не заменяет вхождения других ключей. Если указанный ключ отсутствует, то возвратится пустая строка.

```text
run str {
    CtxSet(`test`, `?value`)
    CtxSet(`param`, `#test# ==`)
    return CtxValue(`param`) + CtxValue(`nop`) + CtxGet(`param`)
}
// #test# ==?value ==
```

