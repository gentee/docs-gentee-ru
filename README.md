---
description: Документация по языку программирования Gentee.
---

# Скриптовый язык программирования Gentee

Gentee является строго-типизированным процедурным языком. В первую очередь, он предназначен для написания скриптов с целью автоматизации повторяющихся действий и процессов на компьютере. Язык имеет простой синтаксис, лёгок в изучении и сопровождении.

**GitHub репозитарий:** [**https://github.com/gentee/gentee**](https://github.com/gentee/gentee)  
**Скачать для Linux, macOS, Windows:** [**https://github.com/gentee/gentee/releases**](https://github.com/gentee/gentee/releases)  
GitHub репозитарий документации: [https://github.com/gentee/docs-gentee-ru](https://github.com/gentee/docs-gentee-ru/)  
Язык разработки: Go

```go
run : ||"Привет, мир!\r\n"
```

```go
run : $ echo "Привет, мир!"
```

```go
run {
    str name = ReadString(`Укажите ваше имя: `)
    Println(`Привет, %{ ?(*name>0, name, `мир`) }!` )
}
```

Хотите посмотреть пример приложения, которое успешно использует язык программирования Gentee? Взгляните на [Eonza](https://www.eonza.org/ru/) - бесплатная кроссплатформенная программа для легкого создания и управления скриптами.

## Документация

* [Gentee Programming language \(English\)](https://docs.gentee.org)
* [Язык программирования Gentee \(Russian\)](https://ru.gentee.org)

