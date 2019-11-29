# Константы

## Предопределенные константы

### CYCLE

Максимальное количество итераций в цикле. По умолчанию, равно 16000000.

### DEPTH

Максимальная вложенность исполняемых блоков. Ограничивает глубину рекурсии. По умолчанию, равно 1000.

### IOTA

Контанта _IOTA_ используется для автоматического вычисления последовательности контант.

```go
const IOTA * 2 {
    ZERO  // 0
    TWO   // 2
    FOUR  // 4
}
```

### SCRIPT

Константа _SCRIPT_ возвращает путь текущего скрипта. Если он не был указан, то возвращается имя _run_.

```go
// compile from file: /home/ak/gentee/scripts/myscript.g
run {
    Println(SCRIPT) // /home/ak/gentee/scripts/myscript.g
}

// compile from memory
run my_best_script {
    Println(SCRIPT) // my_best_script
}
```

