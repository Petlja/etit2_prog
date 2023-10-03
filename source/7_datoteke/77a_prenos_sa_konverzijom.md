# Пренос података са конверзијом

Наредбе за конверзију података подсећају на наредбе за стандардни улаз и излаз, само што имају још један параметар који се наводи на првом месту. То је заправо показивач на датотеку. То омогућава да овим наредбама програму ставимо до знања где смештамо податке, односно одакле их узимамо ако нам је датотека извор података. 

Пример уписивања целобројне променљиве broj у датотеку чији је показивач дефинисан као `FILE *izlaz = fopen("naziv_datoteke.txt", "w")` гласио би:

```c
fprintf(izlaz, "%d ", broj);
```

Читање целобројне променљиве broj из датотеке чији је показивач дефинисан као `FILE* ulaz = fopen("naziv_datoteke.txt", "r")`:

```c
fscanf(ulaz, "%d ", &broj);
```

Функција `fscanf` враћа `EOF` ако је дошло до грешке или до краја датотеке. 

Приликом читања података из датотеке користићемо функцију `feof`.

 Она испитује да ли се приликом читања дошло до краја фајла. 

 ```c
while (!feof(ulaz))
{
    int broj;
    fscanf(ulaz, "%d ", &broj);
    printf("%d", broj);
}
 ```

Значење претходног кода било би:

Све док показивач не дође до краја датотеке, врши се читање садржаја датотеке и смештање у променљиву `broj`. У последњем реду се `broј` штампа на стандардном излазу.

```{questionnote}
Написати програм којим се у текстуалну датотеку `brojevi.txt` врши упис n бројева. Бројеве у датотеци уписати у редовима са по максимално десет бројева **у реду и са размаком између њих**.
```

```c
#include<stdio.h>
int main(void)
{
    FILE* izlaz;
    int i, broj, n;
    izlaz = fopen("brojevi.txt", "w");
    if (izlaz == NULL)
    {
        printf("Greska pri otvaranju fajla!");
        return 1;
    }
    printf("Unesi vrednost za n: ");
    scanf("%d", &n);
    for (i = 0; i < n; i++)
    {
        printf("%d.broj: ", i + 1);
        scanf("%d", &broj);
        fprintf(izlaz, "%3d", broj);
        if ((i + 1) % 10 == 0)
            fprintf(izlaz, "\n");
    }
    fclose(izlaz);
    return 0;
}
```

**Резултат извршавања програма:**

```text
Unesi vrednost za n: 13
1.broj: 1
2.broj: 2
3.broj: 3
4.broj: 4
5.broj: 5
6.broj: 6
7.broj: 7
8.broj: 8
9.broj: 9
10.broj: 10
11.broj: 11
12.broj: 12
13.broj: 13
```

За n = 13 датотека би изгледала овако:

```text
1   2   3   4   5   6   7   8   9  10 
11  12  13
```

Уместо стандардног уноса, због могућности лакшег уноса више бројева можемо користити и функцију за генерисање случајних бројева `rand()` која се налази у заглављу `stdlib.h`.

```c
for (i = 0; i < n; i++)
{
    int broj = rand() % 10; //opseg brojeva 0-9
    fprintf(izlaz, "%3d ", broj);
    if ((i + 1) % 10 == 0)
       fprintf(izlaz, "\n");
}
```

За n = 56 садржај датотеке би изгледао овако:

```text
1  7  4  0  9  4  8  8  2  4
5  5  1  7  1  1  5  2  7  6
1  4  2  3  2  2  1  6  8  5
7  6  1  8  9  2  7  9  5  4
3  1  2  3  3  4  1  1  3  8
7  4  2  7  7  9
```

```{questionnote}
Из датотеке `brojevi.txt` прочитати садржај и приказати га на екрану.
```

```c
#include<stdio.h> 
int main(void)
{
    FILE* ulaz;
    int i = 0, broj;
    ulaz = fopen("brojevi.txt", "r");
    if (ulaz == NULL)
    {
        printf("Greska pri otvaranju fajla");
        return 1;
    }
    while (!feof(ulaz))
    {
        int broj;
        fscanf(ulaz, "%2d ", &broj);
        printf("%3d", broj);
        if ((i + 1) % 10 == 0)
            printf("\n");
        i++; 
    }
    fclose(ulaz);
    return 0;
}
```

**Резултат извршавања програма:**

```text
1  7  4  0  9  4  8  8  2  4
5  5  1  7  1  1  5  2  7  6
1  4  2  3  2  2  1  6  8  5
7  6  1  8  9  2  7  9  5  4
3  1  2  3  3  4  1  1  3  8
7  4  2  7  7  9
```

```{suggestionnote}
У наредним задацима ћемо увежбати датотеке и повезати их са областима до сада обрађеним на курсу *Програмирање 2*. 
```

```{questionnote}
Написати програм којим се уносе подаци о низу особа, а затим одређује која је од унетих особа најстарија. Особе су дефинисане као структуре. Такође је потребно податке о настаријој особи уписати у датотеку *Osoba.txt*.
```

*Објашњење:*

У овом задатку користићемо структуре, низове, стрингове и датотеке.

```c

#include<stdio.h>

typedef struct
{
    char imeiprezime[30];
    int godine;
} Osoba;
 
int main(void) 
{
    int brojOsoba;
    // Deklariranje niza struktura tipa Osoba
    Osoba osobe[20]; 
    Osoba najstariji;
    FILE* izlaz;
    izlaz = fopen("Osoba.txt", "w");
 
    printf("Unesite broj osoba: ");
    scanf("%d", &brojOsoba); 
     
    // Unos podataka za svaku osobu
    for (int i = 0; i < brojOsoba; i++) 
    {
        getchar();//Čisti preostali '\n' karakter iza scanf
        printf("Unesite ime i prezime %d. osobe: ", i + 1);
        gets(osobe[i].imeiprezime);
        printf("Unesite starost %d. osobe: ", i + 1);
        scanf("%d", &osobe[i].godine);
    }
 
    // Pronalaženje najstarije osobe
    najstariji = osobe[0]; // Pretpostavljamo da je prva osoba najstarija
 
    for (int i = 1; i < brojOsoba; i++) 
    {
        if (osobe[i].godine > najstariji.godine) 
            najstariji = osobe[i];         
    }
 
    // Ispis najstarije osobe
    printf("\nNajstarija osoba je:\n");
    printf("Ime i prezime: %s\nGodine: %d\n", najstariji.imeiprezime, najstariji.godine);
    //Upisivanje podataka u datoteku		  
    fprintf(izlaz, "Najstarija osoba je: \n");		
    fprintf(izlaz, "Ime i prezime: %s\nGodine: %d", najstariji.imeiprezime, najstariji.godine);
    fclose(izlaz);
    return 0;
}

```

**Резултат извршавања програма:**

```text
Unesite broj osoba: 3
Unesite ime i prezime 1. osobe: Marko Jovanovic
Unesite starost 1. osobe: 25
Unesite ime i prezime 2. osobe: Vladimir Vucinic
Unesite starost 2. osobe: 14
Unesite ime i prezime 3. osobe: Marija
Unesite starost 3. osobe: 23

Najstarija osoba je:
Ime i prezime: Marko Jovanovic
Godine: 25

```

Датотека *Osoba.txt*

```text
Najstarija osoba je: 
Ime i prezime: Marko Jovanovic
Godine: 25	
```

```{questionnote}
Написати програм који чита из датотеке *Ulaz.txt* име, презиме ученика и број бодова на тесту, а затим уписује податке о ученицима који имају број бодова већи од просека у датотеку *Izlaz.txt*.
```

Датотека *Ulaz.txt*

```text
Marko
Bogdanovic
83.50
Dragana
Babic
31.00
Stevan
Kovacevic
36.00
Vladimir
Vucinic
92.50
Jovana
Komatovic
97.00
```

*Објашњење:*

У овом задатку користићемо структуре, функције и датотеке. У функцији се показивач наводи као било који други тип – `FILE* ulaz`. Приликом позива наводимо само име стварног параметра, показивача `ulaz`.

**Пример:**

*Заглавље функције*:

```c
int citajDat(FILE* ulaz, Ucenik niz[])
```

*Позив у главном програму*:

```c
int n = citajDat(ulaz, niz);
#include<stdio.h>

typedef struct
{
    char ime[20];
    char prezime[30];
    float bodovi;
} Ucenik;
 
 
int citajDat(FILE* ulaz, Ucenik ucenik[])
{
    int i = 0;
    while (!feof(ulaz))
    {
        fscanf(ulaz, "%s%s%f", &ucenik[i].ime, &ucenik[i].prezime, &ucenik[i].bodovi);
        i++;
    }
    return i;//broj ucenika
}

float prosekBodova(Ucenik ucenik[], int n)
{
    float s = 0.0, prosek;
    int i;
    for (i = 0; i < n; i++)
        s += ucenik[i].bodovi;
    prosek = s / n;
    return prosek;
}

void upisDat(FILE* izlaz, Ucenik ucenik[], int n, float prosek)
{
    int i;
    fprintf(izlaz, "Ucenici ciji je broj bodova veci od %.2f su:\n", prosek);
    for (i = 0; i < n; i++)
        if (ucenik[i].bodovi > prosek)
            fprintf(izlaz, "%-20.15s\t%-20.15s\t%.2f\n", ucenik[i].ime, ucenik[i].prezime, ucenik[i].bodovi);
}
 
int main(void)
{
    Ucenik ucenik[20];
    int i, brojUcenika = 0, suma = 0;
    float prosek;
    FILE* ulaz;
 
    ulaz = fopen("Ulaz.txt", "r");
    if (ulaz == NULL)
    {
        printf("Greska pri citanju datoteke!\n");
        return 1;
    }
    FILE* izlaz;
    izlaz = fopen("Izlaz.txt", "w");
    if (izlaz == NULL)
    {
        printf("Greska pri upisu u datoteku!\n");
        return 1;
    }
    int n = citajDat(ulaz, ucenik);
    prosek = prosekBodova(ucenik, n);
    upisDat(izlaz, ucenik, n, prosek);
    fclose(ulaz);
    fclose(izlaz);
    return 0;
}
```

**Резултат извршавања програма**:

Датотека *Izlaz.txt*

```text
Ucenici ciji je broj bodova veci od 68.00 su:
Marko               	Bogdanovic          	83.50
Vladimir            	Vucinic             	92.50
Jovana              	Komatovic           	97.00
```

```{questionnote}
Написати програм којим се креира датотека *matrica.txt* и у њу уписују димензије и елементи матрице у одговарајућем формату.
```

*Објашњење*:

У овом задатку користићемо матрице, функције и датотеке.

```c
#include<stdio.h>

void unosMatrice(FILE* izlaz, int a[][10], int m, int n)
{
    int i, j;
    for (i = 0; i < m; i++)
    {
        for (j = 0; j < n; j++)
        {
            printf("a[%d][%d] = ", i, j);
            scanf("%d", &a[i][j]);
            fprintf(izlaz, "%3d ", a[i][j]);
        }
        fprintf(izlaz, "\n");
    }
}

int main(void)
{
    int a[10][10], m, n;
    FILE* izlaz;
    izlaz = fopen("matrica.txt", "w");
    //kreiranje datoteke matrica.txt
    if (izlaz == NULL)
    {
        printf("Greska!\n");
        return 1;
    }
 
    //ucitavanja dimenzija matrice
    printf("Unesi dimenzije matrice m i n\n");
    scanf("%d %d", &m, &n);
    fprintf(izlaz, "%d %d\n", m, n);
    //ucitavanja elemenata matrice
    printf("\nUnesi elemente matrice:\n");
    unosMatrice(izlaz, a, m, n);
    fclose(izlaz);
    return 0;
}
```

**Резултат извршавања програма**:

```text
Unesi dimenzije matrice m i n
3 4

Unesi elemente matrice:
a[0][0] = 3
a[0][1] = 8
a[0][2] = 41
a[0][3] = 36
a[1][0] = 0
a[1][1] = -39
a[1][2] = 17
a[1][3] = 61
a[2][0] = 86
a[2][1] = 7
a[2][2] = 4
a[2][3] = 32

Датотека *matrica.txt*

```text
3 4
2    6   7  13 
65   8   4  24 
38  95  61  45
```

```{questionnote}
Написати програм за унос елемената матрице `М` димензије `n x n`. Елементе матрице унети у датотеку *matrica.txt*, а у датотеку *zbir.txt* унети суму елемената матрице `М`.
```

*Објашњење*:

У овом задатку користићемо матрице, показиваче, динамичку алокацију меморије, функције и датотеке.

```c
#include<stdio.h>
#include<stdlib.h>

void unosMatrice(FILE* izlaz1, FILE* izlaz2)
{
    int i, j, n, ** M;
    int suma = 0;
    printf("Uneti dimenzije matrice: ");
    scanf("%d", &n);
    M = (int**)malloc(n * sizeof(int*));
    printf("Uneti elemente matrice: ");
    for (i = 0; i < n; i++) 
    {
        *(M + i) = (int*)malloc(n * sizeof(int));
        for (j = 0; j < n; j++)
        {
            fprintf(izlaz1, "%d\t", M[i][j]);
            suma += M[i][j];
        }
        fprintf(izlaz1, "\n");
    }
    fprintf(izlaz2, "Suma elemenata matrice je: %d\n", suma);
}

int main(void)
{
    FILE* izlaz1, * izlaz2;
    izlaz1 = fopen("matrica.txt", "w");
    izlaz2 = fopen("zbir.txt", "w");
    unosMatrice(izlaz1, izlaz2);
    fclose(izlaz1);
    fclose(izlaz2);
    return 0;
}
```

**Резултат извршавања програма**:

```text
Uneti dimenzije matrice: 3
Uneti elemente matrice:
1 2 3 4 5 6 7 8 9

Датотека *matrica.txt*

```text
Uneti dimenzije matrice: 3
Uneti elemente matrice:
1 2 3 
4 5 6 
7 8 9
```

Датотека *zbir.txt*

```text
Suma elemenata matrice je: 45
```

```{questionnote}
Написати програм за читање елемената низа А из датотеке *Niz.txt*. Сортирати елементе низа у растућем поретку и одредити максимални елемент низа. Исписати добијене податке на стандардном излазу и у датотеку *max.txt*.
```

Датотека *Niz.txt*

```text
11 2 32 4 51 6 17 82 9
```

*Објашњење*:

У овом задатку користићемо показиваче, динамичку алокацију меморије,  сортирање, функције и датотеке.

```c
#include<stdio.h>
#include<stdlib.h>

void razmeni(int* a, int* b)
{
    int pom;
    pom = *a;
    *a = *b;
    *b = pom;
}

void sort(int* A, int n)
{
    int i, j;
    for (i = 0;i < n - 1;i++)
        for (j = i + 1;j < n;j++)
            if (*(A + i) > *(A + j))
                razmeni((A + i), (A + j));
}

int citajDat(FILE* ulaz, int* A)
{
    int i = 0;
    while (!feof(ulaz))
    {
        fscanf(ulaz, "%d", (A + i));
        i++;
    }
    return i;
}

int main(void)
{
    FILE* ulaz, * izlaz;
    int* A, n = 0, i, max;
    A = (int*)malloc(80 * sizeof(int));
    ulaz = fopen("Niz.txt", "r");
    if (ulaz == NULL)
    {
        printf("Greska pri citanju datoteke!");
        return 1;
    }
    izlaz = fopen("Max.txt", "w");
    if (izlaz == NULL)
    {
        printf(" Greska!");
        return 1;
    }
    
    n = citajDat(ulaz, A);
    max = *A;
    for (i = 1; i < n; i++)
        if (*(A + i) > max)
            max = *(A + i);
    sort(A, n);
 
    for (i = 0;i < n;i++)
    {
        fprintf(izlaz, "%d\n", *(A + i));
        printf("%d\n", *(A + i));
    }
    fprintf(izlaz, "Maksimalni element niza je %d\n", max);
    printf("Maksimalni element niza je %d\n", max);
    fclose(izlaz);
    fclose(ulaz);
    return 0;
}
 
```

**Резултат извршавања програма**:

```text
2  4  6  9 11 17 32 51 82
Maksimalni element niza je 82
```

Датотека *max.txt*

```text
2  4  6  9 11 17 32 51 82
Maksimalni element niza je 82
```


```{questionnote}
Написати програм којим се уносе подаци о n аутомобила у датотеку *Automobili.txt*. Израчунати просечну вредност задате марке аутомобила и уписати у датотеку *Automobili.txt*. Структура Auto садржи следеће чланове: марка, година производње и цена.
```

*Објашњење*:

У овом задатку користићемо стрингове,  функције и датотеке. 

```c
#include<stdio.h>
#include<string.h>

typedef struct {
    char marka[20];
    int godina;
    float cena;
} Auto;

void unosDat(FILE* izlaz, Auto a[], int n)
{
    int i;
    for (i = 0; i < n; i++) 
    {
        printf("Unesite marku automobila: ");
        scanf("%s", &a[i].marka);
        fprintf(izlaz, "%s ", a[i].marka);
        printf("Unesite godinu proizvodnje automobila: ");
        scanf("%d", &a[i].godina);
        fprintf(izlaz, "%d ", a[i].godina);
        printf("Unesite cenu automobila: ");
        scanf("%f", &a[i].cena);
        fprintf(izlaz, "%.2f ", a[i].cena);
        fprintf(izlaz, "\n");
        printf("\n");
    }
}
float prosecnaCena(Auto a[], int n, char trazenaMarka[])
{
    float s = 0.0, br = 0;
    for (int i = 0; i < n; i++)
        if (strcmp(a[i].marka, trazenaMarka) == 0)
        {
            s = s + a[i].cena;
            br++;
        }
    return s / br;
}

int main(void)
{
    int n;
    float prosecna_cena;
    Auto a[20];
    char marka[20];
    FILE* izlaz;
    izlaz = fopen("automobili.txt", "w");
    if (izlaz == NULL)
    {
        printf("Greska!");
        return 1;
    }
    printf("Unesite broj automobila: ");
    scanf("%d", &n);
    unosDat(izlaz, a, n);
    printf("Unesite marku automobila: ");
    scanf("%s", marka);
    prosecna_cena = prosecnaCena(a, n, marka);
    fprintf(izlaz, "Prosecna cena automobila marke %s je: %.2f\n", marka, prosecna_cena);
    fclose(izlaz);
    return 0;
}
```

**Резултат извршавања програма**:

```text
Unesite broj automobila: 5
Unesite marku automobila: Ford
Unesite godinu proizvodnje automobila: 2012
Unesite cenu automobila: 3700

Unesite marku automobila: Mercedes
Unesite godinu proizvodnje automobila: 2018
Unesite cenu automobila: 11700

Unesite marku automobila: Opel
Unesite godinu proizvodnje automobila: 2007
Unesite cenu automobila: 2300

Unesite marku automobila: Ford
Unesite godinu proizvodnje automobila: 2006
Unesite cenu automobila: 1900

Unesite marku automobila: Ford
Unesite godinu proizvodnje automobila: 2019
Unesite cenu automobila: 6700

Unesite marku automobila cija se trazi prosecna cena: Ford

```

Датотека *Automobili.txt*

```text
Ford 2012 3700.00 
Mercedes 2018 11700.00 
Opel 2007 2300.00 
Ford 2006 1900.00 
Ford 2019 6700.00 
Prosecna cena automobila marke Ford je: 4100.00

```

