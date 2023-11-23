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