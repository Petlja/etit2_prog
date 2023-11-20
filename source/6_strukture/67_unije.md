# Уније

Унија је сложени тип података који омогућава да се у исти меморијски простор у
различитим тренуцима смештају подаци различитих типова. Дефиниција је иста као
код структуре, само што се пише `union` уместо `struct`.

Код структуре у датом моменту сва поља имају дефинисану вредност.

Код уније у датом моменту само једно поље има дефинисану вредност.

Величина структуре се добија када се саберу сва меморијска поља структуре, док
је величина уније величина меморијског поља најширег поља.

Код структуре се за почетне вредности наводе вредности за свако поље, а код
уније се наводи само једна вредност, и то је вредност почетног поља уније.

```c
struct s
{
    int i;
    double d;
    char c;
};
```

```{image} images/image6.png
:width: 220
:align: center
```

```c
union u
{
    int i;
    double d;
    char c;
};
```

```{image} images/image7.png
:width: 180
:align: center
```

Ово наводи на закључак да, када се ради са унијом, морате сачувати претходно
поље уније пре него се замени новим. То се најлакше постиже коришћењем датотека.
```{questionnote}
Написати програм који се дефинише једна структура и једна унија, које садрже три поља `int i`,`float f` и `char str[20]`. На излазу приказати колико меморијског простора саузима структура а колико унија.
```
***Решење:***
```c
#include <stdio.h>
#include <string.h>
struct struktura
{
    int i;
    float f;
    char str[20];
};
union unija
{
    int i;
    float f;
    char str[20];
};
int main( void)
{
    struct struktura podatak_1;
    union unija podatak_2;
    printf( "Zauzeta memorija strukturom je: %d bajta\n", sizeof(podatak_1));
    printf( "Zauzeta memorija unijom je: %d bajta", sizeof(podatak_2));
    return 0;
}
```
**Излаз**:
```text
Zauzeta memorija strukturom je: 28 bajta
Zauzeta memorija unijom je: 20 bajta
```
Приметићемо да је унија заузела 20 бајта што одговара дужини најдужег поља у унији. Дужина структуре одговара збиру бајта који заузимају поља појединачно. 
Погледајмо још један пример:
```c
#include <stdio.h>
#include <string.h>
union unija
{
    int i;
    float f;
    char str[20];
};
int main( void)
{
    union unija podatak;
    podatak.i = 10;
    podatak.f = 220.5;
    strcpy( podatak.str, "C Programiranje");
    printf( "podatak.i : %d\n", podatak.i);
    printf( "podatak.f : %f\n", podatak.f);
    printf( "podatak.str : %s\n", podatak.str);
    return 0;
}
```
**Излаз**:
```text
podatak.i : 1917853763
podatak.f : 4122360580327794900000000000000.000000
podatak.str : C Programiranje
```
Као што можемо видети са излаза поља уније `i` и `f` су недоступна јер поље `str` заузело целу меморијску локацију.

Сада погледајмо измењени пример, где се свака променљива користи у различитим временским тренутцима, што је и сврха коришћења унија. Као што смо на почетку нагласили ово може да буде ефикасно у спрези са датотекама, где се подаци након уноса чувају у датотеци. 
```c
#include <stdio.h>
#include <string.h>
union unija
{
    int i;
    float f;
    char str[20];
};
int main( void)
{
    union unija podatak;
    podatak.i = 10;
    printf( "podatak.i : %d\n", podatak.i);
    podatak.f = 220.5;
    printf( "podatak.f : %f\n", podatak.f);
    strcpy( podatak.str, "C Programiranje");
    printf( "podatak.str : %s\n", podatak.str);
    return 0;
}
```
**Излаз**:
```text
podatak.i : 10
podatak.f : 220.500000
podatak.str : C Programiranje
```
Примећујемо да се сада меморијски простор који заузима промењива `str` користи у различитим временским тренуцима и не долази до преписивања података. 