# Сигнализација грешака

Размотримо мало детаљније функцију `feof`.
Подсетимо се да она испитује да ли се приликом читања дошло до краја датотеке.

Њен облик је:

```c
int feof(datoteka); 
```

Приликом читања података из датотеке, показивач пролази кроз датотеку и као повратну вредност враћа 0. Када дође до краја датотеке, враћа вредност различиту од нуле.

Претходно дефинисане функције употребићемо читајући датотеку по имену *datoteka.txt*. 
Њен садржај је:

```text
Funkcija ftell daje trenutnu vrednost pokazivaca u odnosu na pocetak fajla.
```

```{questionnote}
Прочитати садржај датотеке *datoteka.txt* почевши од 13. знака до краја датотеке.
```

```c
#include<stdio.h>
int main(void)
{
    FILE* ulaz;
    ulaz = fopen("datoteka.txt", "r");
    if (ulaz == NULL)
    {
        printf("Greska pri otvaranju fajla");
        return 1;
    }
    fseek(ulaz, 12, SEEK_SET);
    int p = ftell(ulaz);
    printf("Citamo fajl od %d. pozicije:\n", p + 1);
    while (!feof(ulaz))
    {
        char c;
        c = fgetc(ulaz);
        putchar(c);
    }
    fclose(ulaz);
}
```

**Резултат извршавања програма**:

```text
Citamo fajl od 13. pozicije:
ll daje trenutnu vrednost pokazivaca u odnosu na pocetak fajla.
```

Наредбом `fseek(ulaz, 12, SEEK_SET)` позиционирали смо се после 12. знака јер, подсетимо се, сваки карактер заузима један бајт: 
	
Funkcija `ftell` daje trenutnu vrednost pokazivaca u odnosu na pocetak датотеке.
 
Наредбом `int p = ftell(ulaz)` чита се вредност показивача од почетка датотеке и додељује променљивој p.
Од наредног, 13. знака читамо садржај датотеке до краја. 

```{questionnote}
Прочитати колико има знакова у датотеци *datoteka.txt*.
```

```c
#include<stdio.h>
   int main(void)
{
    FILE* ulaz;
    ulaz = fopen("datoteka.txt", "r");
    if (ulaz == NULL)
    {
        printf("Greska pri otvaranju fajla");
        return 1;
    }
    fseek(ulaz, 0, SEEK_END);
    int p = ftell(ulaz);
    printf("Fajl ima %d karaktera\n", p);
    fclose(ulaz);
}
```

**Резултат извршавања програма**:

```text
Fajl ima 75 karaktera.
```

```{questionnote}
Из датотеке *datoteka.txt* прочитати последња три карактера.
```

```c
#include<stdio.h>
int main(void)
{
    FILE* ulaz;
    ulaz = fopen("datoteka.txt", "r");
    if (ulaz == NULL)
    {
        printf("Greska pri otvaranju fajla");
        return 1;
    }
    fseek(ulaz, -3, SEEK_END);
    while (!feof(ulaz))
    {
        char c;
        c = fgetc(ulaz);
        putchar(c);
    }
    fclose(ulaz);
}
```

**Резултат извршавања програма**:

```text
la.
```

Наредбом `fseek(ulaz, -3, SEEK_END)` показивач је позициониран за три места пре краја датотеке.

Funkcija `ftell` daje trenutnu vrednost pokazivaca u odnosu na pocetak faj|la.

Од те позиције до краја датотеке се чита њен садржај.

## Вежбање

```{mchoice}
:answer1: fscanf - учитавање реда из датотеке
:answer2: fprintf - форматирани упис података у датотеку
:answer3: fputs - упис стринга у датотеку
:answer4: fgetc - учитавање реда из датотеке
:answer5: fputc - уписивање знака у датотеку
:correct: 2,3,5
Дате су функције за рад са датотекама. Поред сваке дат је опис функције. Означи која формулација тачно описује дату функцију.
```

```{mchoice}
:answer1: rewind(dat)
:answer2: fseek(dat, 0, SEEK_CUR)
:answer3: fseek(dat, -1,SEEK_END)
:answer4: ftell(dat)
:answer5: fseek(dat, 0, SEEK_SET)
:correct: 1,5
Дате су наредбе за позиционирање у датотеци. Означи наредбе које служе за позиционирање на почетак датотеке
```

```{mchoice}
:answer1: Даје тренутну вредност показивача од почетка датотеке
:answer2: Испитује да ли се приликом читања дошло до краја датотеке
:answer3: Показивач dat се позиционира на почетак датотеке и омогућава поновно читање и писање
:answer4: Ништа од наведеног
:correct: 3
Заокружи број испред тврдње која тачно описује улогу функције *rewind(dat)* у програму:
```


```{mchoice}
:answer1: Тачно
:answer2: Нетачно
:correct: 1
Дефинисан је низ  int a[50] и показивач на бинарну датотеку dat. 

Означи да ли је следећа тврдња тачна: 

Наредбом `fread(a,sizeof(int), 50, dat)` се чита низ целих бројева дужине 50 из бинарне датотеке:
```

```{mchoice}
:answer1: fwrite(podatak, 2, 1, dat);
:answer2: fprintf(dat, "%2d", podatak);
:answer3: fwrite(&podatak, 2, 1, dat);
:answer4: fwrite(&podatak, 1, 2, dat);
:correct: 3
Декларисани су променљива podatak и показивач dat која представља показивач на бинарну датотеку.

Означи кружић испред исправно написане наредбе којом се 2 бајта уписују у бинарну датотеку:

```