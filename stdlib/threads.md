# Многопоточность

Здесь описаны операторы и функции для работы с потоками \(тип **thread**\).

* [Lock\(\)](threads.md#lock)
* [resume\( thread th \)](threads.md#resume-thread-th)
* [sleep\( int duration \)](threads.md#sleep-int-duration)
* [suspend\( thread th \)](threads.md#suspend-thread-th)
* [terminate\( thread th \)](threads.md#terminate-thread-th)
* [Unlock\(\)](threads.md#unlock)
* [wait\( thread th \)](threads.md#wait-thread-th)
* [WaitAll\(\)](threads.md#waitall)
* [WaitDone\(\)](threads.md#waitdone)
* [WaitGroup\( int count \)](threads.md#waitgroup-int-count)

## Операторы

| Оператор | Результат | Описание |
| :--- | :--- | :--- |
| thread **=** thread |  | Оператор присваивания. |

## Функции

### Lock\(\)

Функция _Lock_ блокирует доступ к глобальному ресурсу (мьютексу). Если он уже занят другим потоком, то текущий поток ждет его освобождения. Мьютекс должен быть освобожден с помощью функции _Unlock_.

### resume\(thread th\)

Функция _resume_ продолжает работу потока, который был остановлен функцией _suspend_.

### sleep\(int duration\)

Функция _sleep_ останавливает выполнение текущего потока на как минимум _duration_ миллисекунд.

### suspend\(thread th\)

Функция _suspend_ приостанавливает поток _th_. Используйте функцию _resume_ для продолжения работы потока.

### terminate\(thread th\)

Функция _terminate_ прекращает работу потока. Если поток уже завершен, то функция ничего не делает.

### Unlock\(\)

Функция _Unlock_ освобождает доступ к глобальному ресурсу (мьютексу). 

### wait\(thread th\)

Функция _wait_ ожидает окончания работы потока _th_. Если поток уже завершен, то функция ничего не делает.

### WaitAll\(\)

Функция _WaitAll_ ожидает когда счётчик _WaitGroup_ станет равен нулю.

```go
run {
  int count = 3
  WaitGroup(count)
  for i in 1..count {
    go {
      // ...
      WaitDone()
    }
  }
  WaitAll()
}
```

### WaitDone\(\)

Функция _WaitDone_ уменьшает счётчик _WaitGroup_ на единицу.

### WaitGroup\(int count\)

Функция _WaitGroup_ создает _WaitGroup_ счётчик потоков, которые должны завершится вызовом функции _WaitDone_. _count_ - начальное значение счётчика.

