

# Время

Здесь описаны операторы и функции для работы с датами и временем \(тип **time**\).

* [int\( time t \) int](time.md#inttime-t-int)
* [time\( int unixtime \) time](time.md#timeint-unixtime-time)
* [AddHours\( time t, int hours \) time](time.md#addhourstime-t-int-hours-time)
* [Date\( int year month day \) time](time.md#dateint-year-month-day-time)
* [DateTime\( int year month day hour minute second \) time](time.md#datetimeint-year-month-day-hour-minute-second-time)
* [Days\( time t \) int](time.md#daystime-t-int)
* [Format\( str layout, time t \) str](time.md#formatstr-layout-time-t-str)
* [Now\( \) time](time.md#now-time)
* [ParseTime\( str layout, str value \) time](time.md#parsetimestr-layout-str-value-time)
* [UTC\( time t \) time](time.md#utctime-t-time)
* [Weekday\( time t \) int](time.md#weekdaytime-t-int)
* [YearDay\( time t \) int](time.md#yeardaytime-t-int)

## Типы

### time

Тип _time_ имеет следующие поля:

* **int Year** - год
* **int Month** - месяц
* **int Day** - день месяца
* **int Hour** - часы
* **int Minute** - минуты
* **int Second** - секунды
* **bool UTC** - если равно _true_, то это UTC время, в противном случае, считается локальное время.

## Операторы

| Оператор | Результат | Описание |
| :--- | :--- | :--- |
| time **==** time | bool | Возвращается _true_, если два времени равны и _false_, в противном случае. |
| time **&gt;** time | bool | Возвращается _true_, если первое время больше чем второе и _false_, в противном случае. |
| time **&lt;** time | bool | Возвращается _true_, если первое время меньше чем второе и _false_, в противном случае. |
| time **!=** time | bool | Возвращается _true_, если два времени не равны и _false_, в противном случае. |
| time **&gt;=** time | bool | Возвращается _true_, если первое время больше или равно второму и _false_, в противном случае. |
| time **&lt;=** time | bool | Возвращается _true_, если первое время меньше или равно второму и _false_, в противном случае. |
| time **=** time | time | Оператор присваивания. |

## Функции

### int\(time t\) int

Функция _int_ конвертирует значение _time_ в Unix время, количество секунд с 1 января 1970 UTC и возвращает его.

### time\(int unixtime\) time

Функция _time_ конвертирует данное Unix время _unixtime_, количество секунд с 1 января 1970 UTC в структуру _time_ и возвращает её.

### AddHours\(time t, int hours\) time

Функция _AddHours_ возвращает новое время, соответствующее указанному, с добавлением _hours_ часов. Параметр _hours_ может быть отрицательным.

### Date\(int year month day\) time

Функция _Date_ возвращает структуру типа _time_ c указанной датой.

### DateTime\(int year month day hour minute second\) time

Функция _DateTime_ возвращает структуру типа _time_ c указанным локальным временем. Также, вы можете инициализировать переменную времени подобным образом

```text
time t = {Year: 2018, Month: 12, Day: 12}
```

### Days\(time t\) int

Функция _Days_ возвращает количество дней в месяце, в котором находится указанное время.

### Format\(str layout, time t\) str

Функция _Format_ возвращает текстовое представление времени в соответствии со строкой _layout_. Функция берет строку токенов и заменяет их соответствующими значениями.

|  | Токен | Вывод |
| :--- | :--- | :--- |
| **Год** | YYYY | 2019 |
|  | YY | 19 |
| **Месяц** | MMMM | January |
|  | MMM | Jan |
|  | MM | 01..12 |
|  | M | 1..12 |
| **День** | DD | 01..31 |
|  | D | 1..31 |
| **День недели** | dddd | Monday |
|  | ddd | Mon |
| **AM/PM** | PM | AM PM |
|  | pm | am pm |
| **Час** | HH | 00..23 |
|  | hh | 01..12 |
|  | h | 1..12 |
| **Минута** | mm | 00..59 |
|  | m | 1..59 |
| **Секунда** | ss | 00..59 |
|  | s | 1..59 |
| **Временная зона** | tz | MST |
|  | zz | -0700 ... +0700 |
|  | z | -07:00 ... +07:00 |

### Now\(\) time

Функция _Now_ возвращает текущее локальное время.

### ParseTime\(str layout, str value\) time

Функция _ParseTime_ разбирает отформатированную строку и возвращает соответствующее время. Список токенов такой же как в функции **Format**.

```text
run str {
  time t &= ParseTime(`MMM D, YYYY at h:mmpm (zz)`, `Jun 7, 2019 at 6:05am (+0300)`)
  time t1 &= ParseTime(`YY/MM/DD HH:mm:s`, `19/05/29 03:21:3`)
  return Format(`YY/MM/DD HH:mm:ss zz`, UTC(t)) + Format(` YY/MM/DD HH:mm:ss`, UTC(t1))
}
// 19/06/07 03:05:00 +0000 19/05/29 03:21:03
```

### UTC\(time t\) time

Функция _UTC_ конвертирует локальное время в UTC и возвращает новую структуру. Если время _t_ уже было UTC, то возвращается его копия.

### Weekday\(time t\) int

Функция _Weekday_ возвращает номер дня недели. 0 - воскресенье, 1 - понедельник и т.д.

### YearDay\(time t\) int

Функция _YearDay_ возвращает номер дня в году у указанного времени.

