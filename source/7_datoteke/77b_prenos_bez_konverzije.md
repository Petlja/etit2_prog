# Пренос података без конверзије

Упознао си се већ са функцијама за читање и исписивање знакова без конверзије. То је било када си обрађивао стрингове. Функције за рад са датотекама имају исто значење само што је извориште, односно одредиште података датотека, а не тастатура и екран.

Направићемо паралелу значења функција:

`fgetc(FILE* datoteka)` – функција чита знак из датотеке *datoteka*

`getchar()` - функција за читање следећег знака преко главног улаза, која као резултат даје кôд прочитаног знака типа `int`

Унаредном програму наредбом *c = fgetc(ulaz)* чита се по један знак из датотеке и штампа на екрану коришћењем наредбе *putchar(c)*. Читање се врши док се не дође до краја датотеке.

```c
#include<stdio.h>
int main(void)
{
    FILE* ulaz;
    int i, broj, n;
    ulaz = fopen("datoteka.txt", "r");
    if (ulaz == NULL)
        printf("Greska pri otvaranju fajla");
    while (!feof(ulaz))
    {
        char c;
        c = fgetc(ulaz);
        putchar(c);
    }
    return 0;
}
```

Датотека *datoteka.txt*

```text
Prenos podataka bez konverzije...
```

**Резултат извршавања програма**:

```text
Prenos podataka bez konverzije...
```

`putchar(c)` – функција за исписивање знака с на екрану

`fputc(с, FILE *датотека)`– ова функција уписује један знак у датотеку

У наредном програму наредбом *c = getchar()* чита се знак са стандардног улаза и уписује у датотеку
наредбом *fputc(c, izlaz)*.

```c
#include<stdio.h>
int main(void)
{
    FILE* izlaz;
    int n;
    izlaz = fopen("datoteka.txt", "w");
    char c;
    c = getchar();
    fputc(c, izlaz);
    fclose(izlaz);
    return 0;
}
```

`gets(s)` - функција за читање једног реда текста и смештање у знаковни низ `s`

`fgets(s, n,FILE *datoteka)` – функција за читање реда из датотеке све до краја реда (до знака `\n`) или док се не прочита `n-1` карактер. Овај низ знакова се смешта у низ `s`. 


```c
#include<stdio.h> 
int main(void)
{
    FILE* ulaz;
    int i, broj, n;
    ulaz = fopen("datoteka.txt", "r");
    char s[100];
    n = 26;
    while (!feof(ulaz))
    {
        fgets(s, n, ulaz);
        puts(s);
    }
}
```

`gets(s)` - функција за читање једног реда текста и смештање у знаковни низ s

`fgets(s, n, FILE *datoteka)` – функција за читање реда из датотеке све до краја реда (до знака `\n`) или док се не прочита `n-1` карактер. Овај низ знакова се смешта у низ `s`. 

```c
#include<stdio.h> 
int main(void)
{
    FILE* ulaz;
    int i, broj, n;
    ulaz = fopen("datoteka.txt", "r");
    char s[100];
    n = 26;
    while (!feof(ulaz))
    {
        fgets(s, n, ulaz);
        puts(s);
    }
}
```

Датотека *datoteka.txt*

```text
fgets je funkcija za citanje reda iz datoteke sve do kraja reda (do znaka \n) ili 
dok se ne procita n-1 karakter. 
Ovaj niz znakova se smesta u niz s.

```

**Резултат извршавања програма**:

```text
fgets je funkcija za cita
nje reda iz datoteke sve
do kraja reda (do znaka \
n) ili
dok se ne procita n-1 kar
akter.
Ovaj niz znakova se smest
a u niz s.
```

```{infonote}
Обрати пажњу да је из датотеке прочитано максимално 25 (n-1) карактера по реду!
```

`puts(s)` - функција за исписивање знаковног низа s, која додаје знак `\n` на крају

`fputs(s, FILE *datoteka)` - исписује стринг s у датотеку уз додавање знака `\n` на крај реда


```c
#include<stdio.h>
int main(void)
{
    FILE* izlaz;
    izlaz = fopen("datoteka.txt", "a");
    char s[50];
    gets(s);
    fputs(s, izlaz);
    fclose(izlaz);
}
```

```{questionnote}
Написати програм који копира садржај датотеке *prva.txt* у датотеку *druga.txt* без брисања постојећих података у другом фајлу.
```

```c
#include<stdio.h>

int main(void)
{
    FILE* ulaz, * izlaz;
    char c;
    ulaz = fopen("prva.txt", "r");
    izlaz = fopen("druga.txt", "a");
    if (ulaz == NULL)
    {
        printf("Greska pri otvaranju fajla");
        return 1;
    }
    if (izlaz == NULL)
    {
        printf("Greska pri otvaranju fajla");
        return 1;
    }
    while ((c = fgetc(ulaz)) != EOF)
        fputc(c, izlaz);
    fclose(ulaz);
    fclose(izlaz);
}
```

Датотека *prva.txt*:

```text
Sadrzaj datoteke prva.txt kopiramo u datoteku druga.txt.
```

**Резултат извршавања програма**:

Датотека *druga.txt*:

```text
Sadrzaj datoteke prva.txt kopiramo u datoteku druga.txt.
```

```{questionnote}
У датотеци *ulaz.txt* се налази низ целих бројева (n < 20). Сваки број се налази у посебном реду. Написати програм којим се исписује низ сортиран у растућем поретку истовремено на екрану и у датотеци *izlaz.txt*.
```

Датотека *ulaz.txt*:

```text
23
145
4
793
-17
53
183
```

```c
#include<stdio.h>
#include<stdlib.h>
void sort(int a[], int n)
{
    int tmp, i, j;
    for (i = 0; i < n - 1; i++)
        for (j = i + 1;j < n;j++)
            if (a[i] > a[j])
            {
                tmp = a[i];
                a[i] = a[j];
                a[j] = tmp;
            }
}

int main(void)
{
    FILE* ulaz, * izlaz;
    char c;
    int a[20], i = 0, n;
    char s[11];
    ulaz = fopen("ulaz.txt", "r");
    izlaz = fopen("izlaz.txt", "w");
    if (ulaz == NULL)
        printf("Greska pri otvaranju fajla");
    if (izlaz == NULL)
        printf("Greska pri otvaranju fajla");
    while (fgets(s, 11, ulaz) != NULL)
        a[i++] = atoi(s);
    n = i;
    sort(a, n);
    for (i = 0; i < n; i++)
    {
        printf("%5d", a[i]);
        fprintf(izlaz, "%5d", a[i]);
    }
    fclose(ulaz);
    fclose(izlaz);
}

```

**Резултат извршавања програма**:

```text
-17   4   23   53  145  183  793
```

Датотека *izlaz.txt*:

```text
-17   4   23   53  145  183  793
```






