# Описания

## Описание констант

Имя константы не должно содержать букв в нижнем регистре. Константам можно присваивать любые выражения. Значение константы вычисляется при первом обращении к данной константе, но тип константы автоматически определяется на этапе компиляции по типу присваиваемого выражения. Поэтому, несмотря на то, что тип при определении константы не указывается, действует проверка типов при её использовании.

```text
ConstDecl      = "const" ( ConstIota | ConstExp )
ConstIota = Expression "{" { IdentifierList newline } "}"
ConstExp = "{" { identifier "=" Expression newline } "}"
```

Константы можно определить двумя способами.

1. Указывая начальное значение или выражение для каждой константы.

   ```text
   const {
    MY_ID = 1
    MY_VAL = myFunc( MY_ID + 23)
    CHECK= MY_VAL < 32
   }
   ```

2. Используя общее выражение с **IOTA**. Иногда возникает необходимость определить список констант со значениями, которые вычисляются по определенным правилам. В этом случае, после ключевого слова **const** необходимо указать одно общее выражение, которая будет вычисляться для каждой константы в данном определении. В этом выражении можно использовать специальную переменную _IOTA_, которая равна порядковому индексу константы в списке с нуля. Сами константы могут перечисляться через пробел или с новой строки.

   ```text
   const 0x1 << IOTA {
      FIRST SECOND   // 0x1    0x2
      THIRD                   // 0x4
   }
   const (IOTA * 2) + 1 {
      MY1    // 1
      MY2   // 3
      MY3   // 5
   }
   ```

## Описание функции

Определение функции состоит из двух частей - описание параметров с возвращаемым типом и тела функции. При определении функции вы должны указать ключевое слово "func", имя функции, передаваемые параметры и тип возвращаемого значения. Только имя функции является обязательным элементом.

```text
FunctionDecl   = "func" FunctionName [Parameters] [ Result ] Block
FunctionName   = identifier 
Result         = TypeName 
Parameters     = "(" [ ParameterList ] ["..."] ")"
ParameterList  = VarList { "," VarList }
```

```text
func VariadicExample(int i, int s...) int {
    int sum = i*2
    for v in s {
       sum += v
    }
    return sum
}
func MyFunc(int par1 par2) int { 
    int par3 = VariadicExample(3, par1, par2, 4, 5, par1+par2)
    return (par1+par2 +par3)/3 
}
```

Заключительный параметр в описании функции может иметь суффикс _'...'_. Функция с таким параметром называется вариативной и может принимать ноль и более аргументов для этого параметра. Вы получаете этот параметр как массив переданных аргументов. Например, _int pars..._ означает, что _pars_ в действительности является _arr.int_ и вы можете получить i-й аргумент с помощью _pars\[i\]_.

## Описание функции запуска

Скрипт на языке Gentee должен содержать специальную функцию без параметров, которая определяется с помощью ключевого слова "run". Выполнение скрипта начинается с вызова этой функции. Скрипт должен иметь только одно определение "run".

```text
RunDecl = "run" [FunctionName] [ Result ] Block
```

```text
run int {
    int i ret
    while i < 10 {
       ret += myFunc(i++)
    }
    return ret
}
```

