# Позиционирања унутар датотеке

Навели смо да функција `fopen` враћа показивач на датотеку, односно да се позиционира на њен почетак. Датотеке у језику `С` су секвенцијалне, а то значи да се подацима приступа по редоследу смештања у датотеку. Осим приступа подацима на почетку датотеке, дозвољено је да се подацима приступи директно унутар датотеке. То представља бржи начин приступа подацима унутар датотеке. Предност директног приступа подацима је та што време приступа неком податку у датотеци не зависи од места на ком се он налази. Програмски језик `C` подржава директан приступ уз једно ограничење: 

-	да бисмо директно приступили неком податку, потребно је да се зна његово одстојање у бајтовима од почетка фајла. 
	Показивач на датотеку дефинисаћемо као `FILE *datoteka`.

## fseek

Функција `fseek` користи се за позиционирање показивача на неко место унутар фајла. 

Њен облик је: 

```c
int fseek(datoteka, pomeraj, odakle)
```

Функција `fseek` омогућава позиционирање у датотеци `datoteka` на место које се за `pomeraj` разликује од позиције дефинисане са `odakle`. 

Вредност `odakle` може бити: 

– `SEEK_CUR`: означава тренутну позицију у датотеци, 

– `SEEK_ЕND`: означава крај фајла, 

– `SEEK_SET`: означава почетак фајла.

**Повратна вредност**

Уколико се функција обави успешно, повратна вредност је једнака 0. У супротном је повратна вредност различита од нуле. 

```{infonote}
Битно је напоменути да функција `fseek` не чита нити уписује податке, она само позиционира показивач!
```


## ftell

Функција `ftell` даје тренутну вредност показивача у односу на почетак фајла. 
Њен облик је: 

```c
ftell(datoteka); 
```

 Резултат ове функције представља број бајтова од почетка фајла до тренутне позиције.


## rewind

Функција rewind враћа позицију показивача на почетак фајла.
Њен облик је:

```c
rewind(datoteka).
```
```{infonote}
У следећем примеру датотека има 41 знак и њен садржај гласи:
*Ovo je primer za funkcije ftell i rewind.*
```

Пример за функције ftell i rewind:
```c
#include<stdio.h>
int main(void)	
{
    FILE *ulaz;
    int i,broj,n;
    ulaz=fopen("datoteka.txt","r");	
    if(ulaz==NULL) 
    {
        printf("Greska!");
        return 1;
    }
//pokazivac se pozicionira na dva mesta do kraja fajla
    fseek(ulaz,-2,SEEK_END);

//ftell vraca broj bajtova od pocetka fajla do trenutne pozicije
    int p=ftell(ulaz); // vraca 39 (41-2)
    printf("%d\n",p);

//rewind vraca pokazivac na pocetak fajla
    rewind(ulaz);
    p=ftell(ulaz);// vraca 0 (pocetak fajla)
    printf("%d\n",p);

//pokazivac se pozicionira na sedam mesta od pocetka fajla
    fseek(ulaz,7,SEEK_SET);
    p=ftell(ulaz); //vraca 7
    printf("%d\n",p);

//pokazivac se pozicionira na tri mesta od trenutne pozicije u fajlu
    fseek(ulaz,3,SEEK_CUR);
    p=ftell(ulaz); //vraca 10 (7+3)
    printf("%d\n",p);
    fclose (ulaz);
    return 0;
}
```
Датотека *datoteka.txt*
```text
Ovo je primer za funkcije ftell i rewind.
```

**Резултат извршавања програма**:

```text
39
0
7
10
```

