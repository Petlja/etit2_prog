# Читање података из бинарне датотеке

Читање података из бинарне датотеке врши се коришћењем наредбе `fread`.
Њен облик је: 

```c
fread(&promenljiva, sizeof(tip_promenljive), broj_promenljivih, dat_promenljiva);
```

Пример – читање једног броја:

```c
float p; 
FILE *ulaz = fopen("ulaz.bin", "rb"); 
fread(&p, sizeof(float), 1, ulaz);
```

Пример – читање низа:

```c
int a[5]; 
fread(a, sizeof(int), 5, ulaz);
```

Приликом читања података из датотеке неопходно је стално проверавати да ли се стигло до краја датотеке. То се ради коришћењем функције `feof(ulaz)`;

```{questionnote}
Уписати један број у бинарну датотеку *broj.dat*.
```

```c
#include<stdio.h>
int main(void)
{
    FILE* izlaz;
    int n, i;
    izlaz = fopen("broj.dat", "wb");
    if (izlaz == NULL)
        printf("greska");
    printf("Unesi broj n = ");
    scanf("%d", &n);
    fwrite(&n, sizeof(int), 1, izlaz);
    fclose(izlaz);
    return 0;
}
```

**Резултат извршавања програма**:

```text
Unesi broj n = 25
```

```{questionnote}
Прочитати садржај датотеке *broj.dat*.
```

```c
#include<stdio.h>
int main(void)
{
    FILE* ulaz;
    int n, i;
    ulaz = fopen("broj.dat", "rb");
    fread(&n, sizeof(int), 1, ulaz); //Citanje brojeva iz datoteke
    printf("%d", n);
    fclose(ulaz);	
}
```

**Резултат извршавања програма**:

```text
n = 25
```

```{questionnote}
Уписати елементе низа у бинарну датотеку *nizbrojeva.dat*.
```

```c
int main(void)
{
    FILE* izlaz;
    int niz[20], n, i;
    izlaz = fopen("nizbrojeva.dat", "wb");
    if (izlaz == NULL)
        printf("greska");
    printf("Koliko ima elemenata u nizu? n = ");
    scanf("%d", &n);
    fwrite(&n, sizeof(int), 1, izlaz); //unosi se duzina niza u datoteku
    printf("Unesite %d elemenata niza:\n", n); //potom se unose elementi niza
    for (i = 0; i < n; i++)
        scanf("%d", &niz[i]);
    fwrite(niz, sizeof(int), n, izlaz); //upis celog niza odjednom
    fclose(izlaz);
    return 0;
}
```

**Резултат извршавања програма**:

```text
Koliko ima elemenata u nizu? n = 5
Unesite 5 elemenata niza:
5
6
9
17
3
```

```{questionnote}
Прочитати садржај датотеке *nizbrojeva.dat*.
```

```c
#include<stdio.h>
int main(void)
{
    FILE* ulaz;
    int niz[20], n, i;
    ulaz = fopen("nizbrojeva.dat", "r+b");
    printf("%d\n", n);
    fread(&n, sizeof(int), 1, ulaz); //Citanje brojeva iz datoteke
    fread(niz, sizeof(int), n, ulaz); //čitanje celog niza
    for (i = 0; i < n; i++)
        printf("niz[%d] = %d\n", i, niz[i]);	
    fclose(ulaz);	
}
```

**Резултат извршавања програма**:

```text
5
niz[0] = 5
niz[1] = 6
niz[2] = 9
niz[3] = 17
niz[4] = 3
```

```{questionnote}
У бинарну датотеку *osoba.dat* уписати податке о особи која је дефинисана као структура. Користити функције.
```

```c
#include<stdio.h>

typedef struct
{
    char ime[20];
    char prezime[20];
    int godine;
} Osoba;

void upisi(Osoba o)
{
    FILE* izlaz = fopen("osoba.dat", "wb");
    fwrite(&o, sizeof(Osoba), 1, izlaz);
    fclose(izlaz);
}

int main(void)
{
    Osoba o = { "Mihailo","Vucinic", 18 };
    upisi(o);
}
```

```{questionnote}
Из бинарне датотеке osoba.dat учитати податке о особи која је дефинисана као структура. Користити функције.
```

```c
#include<stdio.h>

typedef struct
{
    char ime[20];
    char prezime[20];
    int godine;
} Osoba;

Osoba ucitaj()
{
    Osoba o;
    FILE* ulaz = fopen("osoba.dat", "rb");
    fread(&o, sizeof(Osoba), 1, ulaz);
    fclose(ulaz);
    return o;
}

int main(void)
{
    Osoba o;
    o = ucitaj();
    printf("%s %s %d\n", o.ime, o.prezime, o.godine);
}
```

**Резултат извршавања програма**:

Mihailo Vucinic 18

