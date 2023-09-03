# Функције и низови

Приметићеш да смо до сада у функцијама наводили као параметре само просте,
скаларне типове. Међутим, параметри функција могу бити и низови. Честа примена
функција је управо у раду са низовима, како једнодимензионим, тако и
дводимензионим (о овим другим ћеш учити мало касније).

Први проблем који се намеће јесте како копирати све елементе низа у функцију.
Шта ако низ има 100, 500, 1000 елемената? Било би непрактично копирати све те
елементе – то би тражило више времена и меморије.

Решење је да се низови у функцију преносе помоћу адресе, и то адресе првог
елемента низа.

Научили смо да је сâмо име низа адреса првог елемента у низу.

Погледајмо пример:

Креирати функцију zbir која рачуна збир елемената низа.

```c
int zbir(int a[], int n)
{
    int s = 0,i;
    for (i = 0;i < n;i++)
        s = s + a[i];
    return s;
}
```

Као параметри функције наводе се низ и број елемената низа. Када се врши
декларисање функције није битно наводити димензије низа. Програму је битно само
нагласити да је у питању низ, а не прост, скаларни податак.

Приликом позива функције обратити пажњу на следећа правила:

- треба водити рачуна о броју и типу параметара који одговарају функцији,
- на месту параметра које одговара низу треба навести само име низа, никако
не треба стављати заграде `[]`.

```{infonote}
Низ не може бити вредност функције, може бити само параметар
функције. Вредност функције у раду са низовима могу бити само прости, скаларни
подаци.
```

Правилан позив функције у главном програму би могао да изгледа овако:

```c
main()
{
    int a[7] = {1, 2 ,3, 4, 5, 6, 7};
    printf("Suma elemenata niza je %d", zbir(a, 7));
}
```

Капацитет низа који се наводи у главном програму нема значај за функцију. Иста
функција се може позивати за различите димензије низова.

```{infonote}
Да смо декларисали заглавље функције као `int zbir(int n, int a[])`,
на шта се често може наићи, правилан позив би био `zbir(n,a);`

```

Врло често се у раду са низовима креирају функције које не враћају вредности. То
могу бити функције за унос, испис, сортирање, инвертовање елемената низа. Правила
за креирање и позив функције важе и за њих.


```{questionnote}
Креирати функције `unos_niza` и `ispis_niza` којим се уносе и исписују елементи
једнодимензионог низа.
```

**Напомена**: Ове функције ћемо користити и позивати у наредним примерима.

```c
#include<stdio.h>
 
void unos_niza(int a[20], int n)
{
    int i;
    for (i = 0; i < n; i++)
    {
        printf("a[%d] = ", i);
        scanf("%d", &a[i]);
    }
}
void ispis_niza(int a[], int n)
{
    int i;
    printf("\nUneli ste elemente:\n");
    for (i = 0; i < n; i++)
        printf("\n a[%d] = %d", i, a[i]);
    printf("\n");
}

int main(void)
{
    int n, a[20];
    printf("Unesi broj elemenata jednodimenzionalnog niza: ");
    scanf("%d", &n);
    unos_niza(a, n);
    ispis_niza(a, n);
    return 0;
}
```

Резултат извршавања програма:

```text
Unesi broj elemenata jednodimenzionalnog niza: 3
a[0] = 2
a[1] = 9
a[2] = 18

Uneli ste elemente:
a[0] = 2
a[1] = 9
a[2] = 18
```

```{questionnote}
Креирати функцију `invert` и `sort` за инвертовање и сортирање елемената низа.
За сортирање користити методу избора. За унос и испис користити већ формиране
функције `unos_niza` и `ispis_niza`.
```

```c
void invert(int a[], int n)
{
    int i, j, tmp;
    for (i = 0, j = n - 1; i < j; i++, j--)
    {
        tmp = a[i];
        a[i] = a[j];
        a[j] = tmp;
    }
}
 
void sort(int a[], int n) {
    int i, j, tmp;
    for (i = 0; i < n - 1; i++)
        for (j = i + 1; j < n; j++)
            if (a[i] > a[j]) {
                tmp = a[i];
                a[i] = a[j];
                a[j] = tmp;
            }
}
```

За унос и испис низа користићемо већ формиране функције `unos_niza` и `ispis_niza`.
Програм на излазу даће ове резултате:

```{image} images/Picture20.png
:width: 250
:align: center
```

```c
void unos_niza(int a[20], int n)
{
    int i;
    for (i = 0;i < n;i++)
        scanf("%d", &a[i]);
}
void ispis_niza(int a[], int n)
{
    int i;
    for (i = 0;i < n;i++)
        printf("%d ", a[i]);
    printf("\n");
}

int main(void)
{
    int a[50], n;
    printf("Unesi broj elemenata niza n: ");
    scanf("%d", &n);
    unos_niza(a, n);
    printf("Izgled pocetnog niza: \n");
    ispis_niza(a, n);
    invert(a, n);
    printf("Izgled invertovanog niza: \n");
    ispis_niza(a, n);
    sort(a, n);
    printf("Izgled sortiranog niza: \n");
    ispis_niza(a, n);
    return 0;
}
```

```{questionnote}
Дат је низ целих бројева `a[100]`. Креирати функцију у којој се од низа a формира
низ `b` тако што се сви елементи низа `a` који имају парну вредност множе својим
индексом, а сви остали елементи низа a задржавају своју вредност. У главном програму
користити за унос и испис већ формиране функције `unos_niza` и `ispis_niza`.
```

```c
void nizB(int a[], int n)
{
    int k = 0, i, b[50];
    for (i = 0; i < n; i++)
    {
        if (a[i] % 2 == 0)
            b[k++] = a[i] * i;
        else
            b[k++] = a[i];
    }
    ispis_niza(b, k);
}

int main(void)
{
    int a[100], n;
    printf("Unesi broj elemenata niza:\n");
    scanf("%d", &n);
    unos_niza(a, n);
    nizB(a, n);
    return 0;
}
```

Резултат извршавања програма:

```text
Unesi broj elemenata niza:
7
2 8 4 12 3 15 9
0 8 8 36 3 15 9
```

```{questionnote}
Дата су два низа целих бројева `a[50]` и `b[50]`. Креирати функцију којом се формира
нови низ `c` тако што се из низа `a` узму сви непарни елементи, а затим из низа `b` сви
елементи умањени за `2`. Сортирати низ `c` у растућем поретку. У главном програму
користити за унос, испис и сортирање већ формиране функције `unos_niza`, `ispis_niza` и
`sort`. 
```

```c
void nizC(int a[], int b[], int n)
{
    int k = 0, i, c[100];
    for (i = 0; i < n; i++)
    {
        if (a[i] % 2 != 0)
            c[k++] = a[i];
    }
    for (i = 0; i < n; i++)
    {
        c[k++] = b[i] - 2;
    }
    sort(c, k);
    ispis_niza(c, k);
}

int main(void)
{
    int a[50], b[50], c[100], n;
    printf("Unesi broj elemenata niza a i b:\n");
    scanf("%d", &n);
    printf("Unesi niz a:");
    unos_niza(a, n);
    printf("Unesi niz b:");
    unos_niza(b, n);
    nizC(a, b, n);
    return 0;
}
```

## Вежбање

Користећи функције и њихову примену у низовима, решићемо неколико задатака из
Методичке збирке задатака која се налази на Петљи. Решења задатака можеш да
тестираш на сајту.

```{suggestionnote}
У називу задатка се налази линк ка задатку, а у загради страна на којој се налази
задатак у PDF формату збирке.
```

1. [Испис у обратном редоследу](https://petlja.org/biblioteka/r/Zbirka/ispis_u_obratnom_redosledu) (246)

```{questionnote}
Написати програм којим се уноси `n` целих бројева, а затим се унети бројеви приказују
у обратном редоследу од редоследа уношења.
```

**Напомена**: Користићемо прототип функција.

```c
#include<stdio.h>
void unos(int a[20], int n);
void ispis_unazad(int a[], int n);

int main(void)
{
    int n, a[50];
    scanf("%d", &n);
    unos(a, n);
    ispis_unazad(a, n);
    return 0;
}

void unos(int a[20], int n)
{
    int i;
    for (i = 0; i < n; i++)
        scanf("%d", &a[i]);
}

void ispis_unazad(int a[], int n)
{
    int i;
    for (i = n - 1; i >= 0; i--)
        printf("%d ", a[i]);
    printf("\n");
}
```

Резултат извршавања програма:

```text
5 
10 -123 67 14 987
987 14 67 -123 10
```

2. [Најнижа температура](https://petlja.org/biblioteka/r/Zbirka/najmanja_temperatura1) (247)

```{questionnote}
Дате су температуре у неколико градова. Написати програм којим се одређује колика је
температура у најхладнијем граду.
```

```c
#include<stdio.h>
void unos(int a[20], int n)
{
    int i;
    for (i = 0;i < n;i++)
        scanf("%d", &a[i]);
}

int min_temp(int a[], int n)
{
    int min = a[0];
    for (int i = 0;i < n;i++)
        if (a[i] < min)
            min = a[i];
    return min;
}

int main(void)
{
    int n;
    scanf("%d", &n);
    int a[n];
    unos(a, n);
    printf("%d", min_temp(a, n));
    return 0;
}
```

Резултат извршавања програма:

```text
5
10 -12 22 -13 15
-13
```

3. [Минимално одступање од просека](https://petlja.org/biblioteka/r/Zbirka/minimalno_odstupanje_od_proseka) (249)

```{questionnote}
За дати низ од `n` реалних бројева одредити вредност најмањег апсолутног одступања
од просека вредности унетих бројева (то је најмања апсолутна вредност разлика између
елемената и просека низа).
```

**Напомена**: У задатку ћемо користити глобалну променљиву `s` која представља суму елемената низа.
Њој ћемо приступити из обе функције.

```c
#include<stdio.h>
#include<math.h>
double s = 0.0;
void unos(double a[20], int n)
{
    int i;
    for (i = 0; i < n; i++)
    {
        scanf("%lf", &a[i]);
        s = s + a[i];
    }
}

double min_odstupanje(double a[20], int n)
{
    double prosek = s / n;
    double min = fabs(a[0] - prosek);
    for (int i = 1; i < n; i++)
    {
        if (fabs(a[i] - prosek) < min)
            min = fabs(a[i] - prosek);
   }
   return min;
}

int main(void)
{
    int n;
    double a[50];
    scanf("%d", &n);
    unos(a, n);
    printf("%.2lf", min_odstupanje(a, n));
    return 0;
}
```

Резултат извршавања програма:

```text
6
2.8 19.3 -4.2 7.5 -11.1 7.17
0.78
```

4. [Разлика сума до max и од max](https://petlja.org/biblioteka/r/Zbirka/razlika_suma_do_max_i_od_max) (255)

```{questionnote}
Уносе се масе предмета. Одредити разлику суме маса предмета до првог појављивања
предмета највеће масе и суме маса предмета после првог појављивања предмета највеће
масе (предмет највеће масе није укључен ни у једну суму).
```

```c
#include<stdio.h>
void unos(int a[20], int n)
{
    int i;
    for (i = 0; i < n; i++)
        scanf("%d", &a[i]);
}
```

Идеја наредне функције је да врати индекс највећег елемента (његовог првог
појављивања). Ту функцију позваћемо у функције `suma_do_max` и `suma_od_max`.

```c
int max_masa_index(int a[], int n)
{
    int br = 0, k;
    int max = a[0];
    for (int i = 1;i < n;i++)
        if (a[i] > max)
        {
            max = a[i];
            k = i;
        }
    return k;
}
```

Позивањем функције `max_masa_index` добијамо индекс највећег елемента у низу.
Суме елемената низа налазимо до, односно после тог индекса.

```c
int suma_do_max(int a[], int n)
{
    int s = 0, j;
    j = max_masa_index(a, n);
    for (int i = 0; i < j;i++)
        s = s + a[i];
    return s;
}

int suma_od_max(int a[], int n)
{
    int s = 0, j;
    j = max_masa_index(a, n);
    for (int i = j + 1;i < n;i++)
        s = s + a[i];
    return s;
}
 
int main(void)
{
    int n, s1, s2, a[50];
    scanf("%d", &n);
    unos(a, n);
    s1 = suma_do_max(a, n);
    s2 = suma_od_max(a, n);
    printf("%d", s1 - s2);
}
```

Резултат извршавања програма:

```text
5
10 13 7 13 4
-14
```

5. [Максимална разлика суседних](https://petlja.org/biblioteka/r/Zbirka/maksimalna_razlika_susednih1) (275)

```{questionnote}
Написати програм којим се за `n` учитаних целих бројева одређује по апсолутној вредности
највећа разлика два суседна елемента.
```

```c
#include<stdio.h>
#include<math.h>
void unos(int a[20], int n)
{
    int i;
    for (i = 0;i < n;i++)
        scanf("%d", &a[i]);
}

int max_razlika(int a[], int n)
{
    int max = abs(a[0] - a[1]);
    for (int i = 1;i < n - 1;i++)
        if (abs(a[i] - a[i + 1]) > max)
            max = abs(a[i] - a[i + 1]);
    return max;
}

int main(void)
{
    int n, a[50];
    scanf("%d", &n);
    unos(a, n);
    printf("%d", max_razlika(a, n));
    return 0;
}
```

Резултат извршавања програма:

```text
5
-20 30 5 90 70
85
```
