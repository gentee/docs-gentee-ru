# Выражения

Выражение возвращает значение путем применения операторов и функций к операндам. Операндом может быть литерал, идентификатор определяющий константу, переменную, функцию или выражение в скобках. Для вызова функции необходимо указать её имя и в круглых скобках перечислить параметры через запятую. Параметры тоже могут быть выражениями. Кроме этого, можно выносить первый параметр впереди функции и отделять его точкой. Это помогает более наглядно указать последовательность вызовов функций. 
``` go
(b*c).func3(d).func2(a).func1(10)
"my string".Upper().TrimRight("g")
// эквивалентно
func1(func2(func3( b*c, d ), a), 10)
TrimRight(Upper("my string"), "g")
```

```text
Operand     = Literal | OperandName | "(" Expression ")" | GoStmt
Literal     = BasicLiteral
constLit    = "true" | "false"
BasicLiteral    = float | integer | stringLit | constLit | charLit
OperandName = identifier | EnvVariable | FnIdent
PrimaryExpr = Operand | FuncName Arguments | Expression "." FuncName Arguments | IfOp | 
              IndexExp | FieldExpr
OptionalArgs = identifier ":" Expression { "," identifier ":" Expression }
Arguments    = "(" [ ExpressionList ] [ OptionalArgs ] ")" 
ExpressionList = Expression { "," Expression } 
Expression = UnaryExpr | Expression binaryOp Expression | 
             OperandName assignOp Expression
UnaryExpr  = PrimaryExpr | unaryOp UnaryExpr | incOp OperandName | OperandName incOp | 
             UnaryExpr postunaryOp
binaryOp  = "||" | "&&" | relOp | mathOp | assignOp | rangeOp
relOp     = "==" | "!=" | "<" | "<=" | ">" | ">=" 
mathOp   = "+" | "-" | "|" | "^" | "*" | "/" | "%" | "<<" | ">>" | "&" | 
unaryOp  = "-" | "!" | "^" | "*" | "#" | "##"
postunaryOp = "?"
incOp    = "++" | "--" 
rangeOp  = ".."
assignOp = "=" | "+=" | "-=" | "|=" | "^=" | "*=" | "/=" | "%=" | "<<=" | 
           ">>=" | "&=" | "#=" 
IfOp = "?" "(" Expression "," Expression "," Expression ")"
```

При вычислении логических операторов "&&" \(И\) и "\|\|" \(ИЛИ\), правый операнд вычисляется опционально. Например, в случаях `false && myFunc()` и `true || myFunc()` функция myFunc не будет вызываться.

Операторы присваивания являются бинарными операторами, которые возвращают присвоенное значение. Таким образом операторы присваивания могут использоваться внутри выражений.

```go
int i j k
i = j = 5+(k=60/5)*2
return (k+j)*2 + i   // 111
```

## Приоритеты операторов

Как правило все операторы выполняются слева направо, но имеется такое понятие как приоритет операторов. Если следующий оператор имеет более высокий приоритет, то вначале выполнится оператор с более высоким приоритетом. Например, умножение имеет более высокий приоритет и 4 + 5 _2 равно 14, но если мы поставим круглые скобки то \( 4 + 5 \)_ 2 равно 18.

| Оператор | Тип | Ассоциативность |
| :--- | :--- | :--- |
| Высший приоритет |  |  |
| \(   \)  \[   \] |  | Слева направо |
| -   ^   \#   \#\#   \*   ++   -- | Унарный префикс | Справа налево |
| ? | Унарный постфикс | Справа налево |
| ! | Унарный префикс | Справа налево |
| ++   -- | Унарный постфикс | Слева направо |
| /   %   \* | Бинарный | Слева направо |
| +   - | Бинарный | Слева направо |
| &lt;&lt;   &gt;&gt; | Бинарный | Слева направо |
| & | Бинарный | Слева направо |
| ^ | Бинарный | Слева направо |
| \| | Бинарный | Слева направо |
| ==   !=   &lt;   &lt;=   &gt;   &gt;= | Бинарный | Слева направо |
| \|\| | Бинарный | Слева направо |
| && | Бинарный | Слева направо |
| \#= | Бинарный | Слева направо |
| =   +=   -=   \*=   /=   %=   &lt;&lt;=   &gt;&gt;=   &=   ^=   \|= | Бинарный | Справа налево |
| .. | Бинарный | Слева направо |
| Низший приоритет |  |  |

Круглые скобки \(\) изменяют порядок вычисления частей выражения. Операции инкремента ++ и -- могут быть как префиксными, так и постфиксными.

## Условный оператор "?"

Условный оператор "?" аналогичен по своей работе конструкции "if", но может использоваться внутри выражения. Он содержит три операнда-выражения. Операнды заключены в скобки и разделены запятыми, вначале вычисляется значение первого логического \(целочисленного\) выражения. Если значение истинно, то вычисляется второе выражение и полученное значение становится результатом работы условного оператора. В противном случае вычисляется третий операнд и возвращается его значение.

```go
if a >= ?( x, 0xFFF, ?( y < 5 && y > 2, y, 2*b )) + 2345
{
     r = ?( a == 10, a, a + b ) 
}
```

## Инициализация массивов и структур

При определении переменных с типом _arr_, _set_, _buf_ или _map_ можно сразу присвоить элементы массива. Также можно указывать значения полей переменных структурных типов. Значения перечисляются через запятую или перенос строки. В качестве значения можно указывать выражения. При инициализации ассоциативного массива _map_ необходимо указать ключ в виде строки и через двоеточие значение. Если элементами массива являются другие массивы, то они тоже инициализируются с помощью фигурных скобок. При инициализации полей структур необходимо указать ключ в виде идентификатора и через двоеточие значение. Переменная типа **buf** может инициализироваться комбинацией значений типов **int**, **str**, **char**, **buf**.

```text
DelimInit = "," | newline
ArrInit = "{" VarInit {DelimInit VarInit} "}"
BufInit = "{" Expression {DelimInit Expression} "}"
MapInit = "{" Expression ":" VarInit { DelimInit Expression ":" VarInit  }  "}"
SetInit = "{" Expression {DelimInit Expression} "}"
StructInit = "{" identifier ":" VarInit { DelimInit identifier ":" VarInit  }  "}"
VarInit = ArrInit | BufInit | MapInit | StructInit | SetInit | Expression
```

```go
mystruct my = {ID: 20, name: "some text"}
buf a = {250+5, '1', 'A', "test", 0}
map.arr.int ret = {"key1": {0, 1 }, `key2`:{ 2, 3 } }
arr.map ret = { {"test": "value 1"}
                {`next`:"value 2"} }
arr.bool mb = : true, false, true
map  my = {"key1": GetVal(1), "key2": GetVal(2)}
set s &= {1, 0, 45, myintval, MYCONST}
```

## Индексное выражение

Индексы позволяют вам получать или устанавливать определенный элемент переменной по его индексу. Индекс - это позиция определенного элемента внутри указанной переменной. Индексы в Gentee начинаются с нуля \(для **map** индексы имеют строковый тип\), первый элемент имеет индекс 0, второй индекс один и т.д. Следующие типы поддерживают индексы:

* **str**. Индекс должен иметь тип **int** и быть меньше длины строки. Если индекс выходит за этот диапазон, то возникает ошибка выполнения. Результат имеет тип **char**.
* **buf**. Индекс должен иметь тип **int** и быть меньше длины массива. Если индекс выходит за этот диапазон, то возникает ошибка выполнения. Результат имеет тип **int**, но 0 &lt;= значение &lt;= 255.
* **arr**. Индекс должен иметь тип **int** и быть меньше длины массива. Если индекс выходит за этот диапазон, то возникает ошибка выполнения. Результат имеет такой же тип, как тип элементов массива.
* **map**. Индекс должен иметь тип **str**. В случае получения значения, элемент с таким индексом должен существовать в ассоциативном массиве. Если такой ключ отсутствует, то возникает ошибка выполнения. Результат имеет такой же тип, как тип элементов ассоциативного массива.
* **set**. Индекс должен иметь тип **int** и быть меньше 64000000. Если индекс выходит за этот диапазон, то возникает ошибка выполнения. Результат имеет логический тип.

Если массив _array_ или _map_ состоит из массивов, то вы можете последовательно применить индексные выражения.

```text
IndexExp = PrimaryExpr "[" Expression "]" { "[" Expression "]" }
```

```go
str temp = `0123`
temp[1] = temp[3]  // result `0323`
arr ain
ain += `test`
temp = ain[0]
map mymap
mymap["mykey"] = "myvalue"
arr.map amap
amap += mymap
amap[0]["mykey"] = "new value"
```

## Выражения присваивания

Для всех типов в языке Gentee существует оператор присваивания **=**. При использовании присваивания для типов **buf, arr, map, set** и всех структурных типов вы будете получать копии данных. Рассмотрим пример

```go
arr a1 = {`A`, `B`, `C`}
arr a2 = a1
a2 += `D`
a1[0] = `Z`
//  a1 = `Z`, `B`, `C`
//  a2 = `A`, `B`, `C`, `D`
```

При присваивании _a2 = a1_ мы получили копию массива _a1_. Действия над массивами никак не будут влиять друг на друга. Иногда создание копий больших объектов может замедлять выполнение программы. Например, если функция возвращает какую-то структуру, с которой нужно работать дальше, то нет смысла создавать её копию. Для разрешения таких ситуаций, для типов **buf, arr, map, set** и всех структурных типов имеется еще один оператор присваивания **&=**. Этот оператор не копирует данные в переменную, а создает клон этих данных. В этом случае, данные остаются в единственном экземпляре.

```go
arr a1 = {`A`, `B`, `C`}
arr a2 &= a1
a2 += `D`
a1[0] = `Z`
//  a1 = `Z`, `B`, `C`, `D`
//  a2 = `Z`, `B`, `C`, `D`
```

```go
time t
t &= Now()  // так лучше, чем  t = Now()
```

## Контекст

В языке Gentee отсутствуют глобальные переменные. Вместо них имеется ассоциативный массив _map.str_, который доступен на чтение и запись из любых функций и потоков. Кроме хранения данных в виде ключ-значение, контекст может ещё производить рекурсивную замену ключей в строках вида _"\#key\_name\# \#another\_key\_name\#"_. Все [функции для работы с контекстом](https://gentee.github.io/docs-gentee-ru/stdlib/context) описаны в стандартной библиотеке. Здесь рассмотрим только операторы.

* Унарный оператор **\#\# str** рекурсивно заменяет ключи на их значения  в переданной строке и возвращает полученный результат. 
* Унарный оператор **\# key** работает аналогично оператору **\#\#**, но ему нужно передать имя-идентификатор ключа контекста.
* Оператор **key \#= value** записывает в контекст  ключ _key_ с указанным  значением. Если вместо типа _str_ значение имеет тип _int, bool, float_, то оно будет сконвертировано в строку.

```go
func ooops() {
    AB #= `oops`
}
run str {
    AB #= `test`
    CD #= `#AB# - `    // don't replace #AB#.  CD = #AB# - 
    E #= #AB           // get #AB#. E = test
    ooops()            // change AB
    val #= 10
    return #CD + #E + ##` #val# == 10`
}
// Result:  oops - test 10 == 10
```

