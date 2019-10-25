# Дополнительные возможности

## Как добавить свои функции в стандартную библиотеку

При использовании **Gentee** в других проектах может возникнуть потребность в расширении стандартной библиотеки. Функция **Customize** позволяет добавить любое количество go-функций в стандартную библиотеку и использовать их в скриптах. Следует заметить, что в этом случае скрипты не будут компилироваться оригинальным компилятором, так как там будут отсутствовать добавленные функции. Функцию **Customize** необходимо вызвать до вызова прочих функций из пакета gentee.

Для расширения стандартной библиотеки необходимо указать массив функций в параметрe типа [*Custom*](reference.md#type-custom). Каждая функция описывается структурой [*EmbedItem*](reference.md#type-embed-item), в которой указывается прототип на языке Gentee и сама функция. Функция может возвращать значение типа *error* и иметь переменное количество параметров.

### Соответствие типов

Параметры и возвращаемое значение подключаемых go-функций должны иметь типы в соответствии с данной таблицей. При использовании *core* типов необходимо импортировать *github.com/gentee/gentee/core*.

| Gentee тип | Golang тип |
| :--- | :--- | :--- |
| int | int64 |
| bool | int64 |
| char | int64 |
| thread | int64 |
| float | float64 |
| str | string |
| arr | *core.Array |
| buf | *core.Buffer |
| map | *core.Map |
| set | *core.Set |
| struct type | *core.Struct |

```go
func sum(x, y int64) int64 {
	return x + 2*y
}

func varInt(init int64, pars ...int64) int64 {
	for _, i := range pars {
		init += i
	}
	return init
}

func shortLen(s string) (int64, error) {
	if len(s) < 10 {
		return len(s), nil
	}
	return 0, fmt.Errorf("string %s is too long", s)
}

func main() {
    var customLib = []gentee.EmbedItem{
        {Prototype: `sum(int,int) int`, Object: sum},
        {Prototype: `InitSum(int) int`, Object: varInt},
        {Prototype: `ShortLen(str) int`, Object: shortLen},
    }
    err := gentee.Customize(&gentee.Custom{
		Embedded: customLib,
	})
	if err != nil {
		log.Fatal(err)
    }
    workspace := gentee.New()
    exec, _, err := workspace.Compile(`run {
    Println("Sum = %{sum(10, 6)}")
    Println("InitSum = " + InitSum(4, 67, 4, 22))
    ShortLen("this string is too long")
}`, ``)
    ...
}
```