# Обработка ошибок

### Конструкция try catch

По умолчанию, если в момент выполнения скрипта была получена ошибка, то скрипт сразу заканчивает свою работу. Если вы хотите избежать прекращения работы скрипта, то вы должны использовать конструкцию **try**. Если во время выполнения кода внутри блока _try_ произошла ошибка, то управление перейдет в конструкцию **catch**, которая должна быть после **try**. После ключевого слова _catch_ необходимо указать имя переменной типа _error_, которая будет содержать информацию об ошибке. Вы можете использовать [специальные функции](https://gentee.github.io/docs-gentee-ru/stdlib/runtime#erriderror-err-int) для получения идентификатора и текста ошибки. Если вы не удалите ошибку внутри _catch_ с помощью **recover** или **retry**, то она будет передана дальше и скрипт закончит свою работу.

```text
TryStmt ="try" Block CatchStmt
CatchStmt = "catch" identifier Block
```

```text
run  {
   try {
      myfunc()
      error(101, "Custom error")
   }
   catch err {
      if ErrID(err) != 101:  error( 102, 
         "Error \{ErrText(err)} has occurred in myfunc()")
   } 
}
```

### Конструкция recover

Конструкция **recover** используется внутри блока **catch** для удаления ошибки. По этой команде информация об ошибке удаляется, скрипт выходит из текущего блока _catch_ и продолжает выполнение дальше.

```text
RecoverStmt = "recover"
```

```text
run str {
   try : 10/0
   catch err :  recover
   return "ok"
} 
// ok
```

### Конструкция retry

Конструкция **retry** используется внутри блока **catch** для повторного запуска **try**. По этой команде информация об ошибке удаляется и скрипт заново выполняет соответствующий блок _try_.

```text
RetryStmt = "retry"
```

```text
run {
   str fname
   try {
       fname = ReadString("Specify filename: ")
       Println("Beginning of the file: ", str(ReadFile(fname, 0, 50)))
    } catch err {
       Println("ERROR #\{ErrID(err)}: \{ErrText(err)}")
       retry
    }
}
```

## 

