---
nav: tocru
---

# Числа с плавающей точкой

Здесь описаны операторы и функции для работы с действительными числами типа **float**.

* [bool\( float f \) bool](float.md#boolfloat-f-bool)
* [Ceil\( float f \) int](float.md#ceilfloat-f-int)
* [Floor\( float f \) int](float.md#floorfloat-f-int)
* [int\( float f \) int](float.md#intfloat-f-int)
* [Max\( float fl, float fr \) float](float.md#maxfloat-fl-float-fr-float)
* [Min\( float fl, float fr \) float](float.md#minfloat-fl-float-fr-float)
* [Round\( float f \) int](float.md#roundfloat-f-int)
* [Round\( float f, int digit \) float](float.md#roundfloat-f-int-digit-float)
* [str\( float f \) str](float.md#strfloat-f-str)

## Операторы

| Оператор | Результат | Описание |
| :--- | :--- | :--- |
| float **+** float | float | Сложение двух чисел. |
| float **+** int | float |  |
| int **+** float | float |  |
| float **-** float | float | Вычитание второго числа из первого. |
| float **-** int | float |  |
| int **-** float | float |  |
| float **\*** float | float | Умножение двух чисел. |
| float **\*** int | float |  |
| int **\*** float | float |  |
| float **/** float | float | Деление двух чисел. При делении на ноль возвращается ошибка. |
| float **/** int | float |  |
| int **/** float | float |  |
| float **==** float | bool | Возвращает _true_ если два числа равны и _false_, в противном случае. |
| float **==** int | bool |  |
| float **&gt;** float | bool | Возвращает _true_ если первое число больше второго и _false_, в противном случае. |
| float **&gt;** int | bool |  |
| float **&lt;** float | bool | Возвращает _true_ если первое число меньше второго и _false_, в противном случае. |
| float **&lt;** int | bool |  |
| float **!=** float | bool | Возвращает _true_ если два числа не равны и _false_, в противном случае. |
| float **!=** int | bool |  |
| float **&gt;=** float | bool | Возвращает _true_ если первое число больше или равно второму и _false_, в противном случае. |
| float **&gt;=** int | bool |  |
| float **&lt;=** float | bool | Возвращает _true_ если первое число меньше или равно второму и _false_, в противном случае. |
| float **&lt;=** int | bool |  |
| **-** float | float | Смена знака. |
| float **=** float | float | Присваивание. |
| float **+=** float | float | Сложение и присваивание действительных чисел с плавающей точкой. |
| float **-=** float | float | Вычитание и присваивание действительных чисел с плавающей точкой. |
| float **/=** float | float | Деление и присваивание действительных чисел с плавающей точкой. |
| float **\*=** float | float | Умножение и присваивание действительных чисел с плавающей точкой. |

## Функции

### bool\(float f\) bool

Функция _bool_ возвращает _false_, если передаваемый параметр равен 0.0, в противном случае, возвращается _true_.

### int\(float f\) int

Функция _int_ преобразует действительное число с плавающей точкой в целое число типа _int_, которое меньше или равно данному числу.

### str\(float f\) str

Функция _str_ преобразует действительное число с плавающей точкой в строку.

### Ceil\(float f\) int

Функция _Ceil_ возвращает наименьшее целое число, которое больше или равно _f_.

### Floor\(float f\) int

Функция _Floor_ наибольшее целое число, которое меньше или равно _f_.

### Max\(float fl, float fr\) float

Функция _Max_ возвращает максимальное из двух значений.

### Min\(float fl, float fr\) float

Функция _Min_ возвращает минимальное из двух значений.

### Round\(float f\) int

Функция _Round_ округляет _f_ до ближайшего целого.

```text
   Round(4.5) // 5
   Round(4.1) // 4
   Round(4.9) // 5
```

### Round\(float f, int digit\) float

Функция _Round_ округляет действительное число до указанного количества десятичных знаков.

```text
   Round(4.567, 2) // 4.57
   Round(4.111, 1) // 4.1
```

