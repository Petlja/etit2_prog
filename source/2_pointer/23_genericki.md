# Генерички показивачи

До сада смо разматрали показиваче на податке познатих типова. Осим њих постоје и генерички показивачи код којих није дефинисан тип показиваних података. Код њих се уместо типа показиваних података ставља службена реч ``void``. 

С обзиром на то да није одређен тип података на који генерички показивач указује, њима се не може приступити. Да би ово било могуће, неопходно је генерички показивач конверзијом претворити у показивач на познати тип податка.

Погледајмо следећи пример: 

```c
#include<stdio.h>
main()
{
	int a = 8;
	void *pa;
	pa = &a;
	*pa = 23;
	printf("a = %d", a);
}
```

После ове наредбе ће програм јавити грешку. Зашто? Из разлога што је ``pа`` генерички показивач, а помоћу њега желимо да приступимо целобројној променљивој.

Овај проблем ћемо решити употребом оператора за конверзију `*(int*)pa = 23`

```c
#include<stdio.h>
main()
{
	int a = 8;
	void* pa;
	pa = &a;
	*(int*)pa = 23;
	printf("a = %d", a);
}
```

Заправо, овде смо кастовањем генерички показивач претворили у показивач на тип податка типа ``int``. 

Покушај да анализираш следећи код:

```c
float a = 8.50, b = 5.20;
float *pa;
void *pb;
pa = &a;
pb = pa;
*pb = 11.45;
```

```{mchoice}
:answer1: а = 8.50, b = 5.20
:answer2: а = 11.45, b = 5.20
:answer3: а = 11.45, b = 11.45
:answer4: Програм неће приказати вредности, пријавиће грешку.
:correct: 4
Које ће вредности на излазу имати променљиве a и b?
```

*Програм ће пријавити грешку, јер је `*pb` генерички показивач. Грешка
се отклања заменом наредбе `*pb = 11.45` са `*(float*)pb = 11.45`. Вредности
променљивих су a = 11.45, b = 5.20.*
