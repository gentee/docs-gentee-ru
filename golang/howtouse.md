# Компиляция и выполнение

Рассмотрим как использовать компилятор и виртуальную машину Gentee в проектах на языке программирования **Go**.

## Компиляция

Для начала, нужно создать структуру *Gentee* с помощью функции **New**. Эта структура будет хранить всю информацию о скомпилированных скриптах. Вам достаточно создать один экземпляр и компилировать любое количество скриптов.

Для компиляции скриптов нужно использовать методы **Compile**, **CompileFile**, **CompileAndRun**. 
Методы *Compile*, *CompileFile*, в случае успешной компиляции, возвращают структуру *Exec*, которая содержит байт-код. Вы можете сохранять или передавать эту структуру для дальнейшего выполнения с помощью метода **Run**. Метод *CompileAndRun* сразу после компиляции выполняет скрипт и возвращает его результат. 

```go
package main
import (
    "fmt"
    "log"

    "github.com/gentee/gentee"
)

func main() {
    g := gentee.New()

    exec,_, err := g.Compile("run : Print(`Hello, world!`)", "")
    if err != nil {
        log.Fatal(err)
    }
    exec.Run(gentee.Settings{})
    exec,_, err = g.CompileFile("/home/ak/scripts/myscript.g")
    if err != nil {
        log.Fatal(err)
    }
    exec.Run(gentee.Settings{})

    var result interface{}
    result, err = g.CompileAndRun("../torun.g")
    fmt.Println(`Error:`, err, `Result:`, result)
}
```

## Выполнение байт-кода

Готовый байт-код скрипта хранится в структуре типа **Exec**. Для его выполнения необходимо вызвать метод **Run**. Параметр типа [**Settings**](reference.md#type-settings) позволяет передать параметры командной строки и указать дополнительные настройки виртуальной машины.

```go
package main
import (
    "fmt"
    "log"

    "github.com/gentee/gentee"
)

func main() {
    g := gentee.New()

    exec,_, err := g.CompileFile("myscript.g")
    if err != nil {
        log.Fatal(err)
    }
    var result interface{}
    result, err = exec.Run(gentee.Settings{
        CmdLine: []string{
            "-par1",
            "-o",
            "/home/ak/tmp",
        },
    })
    fmt.Println(`Error:`, err, `Result:`, result)
}

```


