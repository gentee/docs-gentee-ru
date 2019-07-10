# Многопоточность

Здесь описаны операторы и функции для работы с потоками \(тип **thread**\).

* [resume\( thread th \)](threads.md#resume-thread-th)
* [sleep\( int duration \)](threads.md#sleep-int-duration)
* [suspend\( thread th \)](threads.md#suspend-thread-th)
* [terminate\( thread th \)](threads.md#terminate-thread-th)
* [wait\( thread th \)](threads.md#wait-thread-th)

## Операторы

| Оператор | Результат | Описание |
| :--- | :--- | :--- |
| thread **=** thread |  | Оператор присваивания. |

## Функции

### resume\(thread th\)

Функция _resume_ продолжает работу потока, который был остановлен функцией _suspend_.

### sleep\(int duration\)

Функция _sleep_ останавливает выполнение текущего потока на как минимум _duration_ миллисекунд.

### suspend\(thread th\)

Функция _suspend_ приостанавливает поток _th_. Используйте функцию _resume_ для продолжения работы потока.

### terminate\(thread th\)

Функция _terminate_ прекращает работу потока. Если поток уже завершен, то функция ничего не делает.

### wait\(thread th\)

Функция _wait_ ожидает окончания работы потока _th_. Если поток уже завершен, то функция ничего не делает.

