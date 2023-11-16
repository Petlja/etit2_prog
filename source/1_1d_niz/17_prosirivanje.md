# Проширивање (експандовање) низа

```{infonote}
Проширивање представља уметање нових чланова низа на жељеној позицији.
```
Следи део кода којим се врши уметање новог члана ``к`` на позицији ``ј`` 

```c
    printf("Unesi poziciju: ");
    scanf("%d", &j);
    printf("Unesi element koji umeces: ");
    scanf("%d", &k);
    for (i = n; i > j - 1; i--)
        a[i] = a[i - 1];
    a[j - 1] = k;
```
Као што нам је познато индекс последњег елемента у низу је ``n-1``. То значи да уколико проширујемо низ за један елемент, индекс последњег елемента ће бити ``n``. Зато у овом циклусу ``i`` крећемо од ``n`` и вршимо пребацивање вредности из елемената са индексом ``i-1`` у елементе са индексом ``i``. На крају у елеменат са индексом на позицији ``j`` уписујемо вредност елемента који се умеће. То значи да ће на крају број елемената ће бити ``n+1``.

```{questionnote}
Иницијализујте један низ од шест целобројних елемената
a[6] = {1, 5, 3, 2, 4, 6}. Проширите га додавањем једног елемента на позицији 2
(на индекс 1). Користећи претходно наведени део кода напишите програм за проширивање.
```

```c
#include <stdio.h> 
int main(void)
{
    int a[7] = {1, 5, 3, 2, 4, 6}, i, j = 2, k;
    printf("\nUneti niz:\n");
    for (i = 0; i < 6; i++)
        printf("a[%d] = %d\n", i, a[i]);
    printf("Unesi element koji umeces: ");
    scanf("%d", &k);
    for (i = 6; i > j - 1; i--)
        a[i] = a[i - 1];
    a[j - 1] = k;
    printf("\nProsireni niz izgleda ovako:\n");
    for (i = 0; i < 7; i++)
        printf("a[%d] = %d\n", i, a[i]);
}
```

**Излаз**:

```text
Uneti niz:
a[0] = 1
a[1] = 5
a[2] = 3
a[3] = 2
a[4] = 4
a[5] = 6
Unesi poziciju: 2
Unesi elemenat koji umeces: 0

Prosireni niz izgleda izgleda ovako:
a[0] = 1
a[1] = 0
a[2] = 5
a[3] = 3
a[4] = 2
a[5] = 4
a[6] = 6
```

Хајде да анализирамо шта се налази у циклусу. Унели смо да се додаје елемент
``k = 0`` на позицији ``j = 2``.

```{image} images/Picture69.svg
:scale: 30
:align: center
```

```{image} images/Picture70.svg
:scale: 30
:align: center
```

```{image} images/Picture71.svg
:scale: 30
:align: center
```

```{image} images/Picture72.svg
:scale: 30
:align: center
```

```{image} images/Picture73.svg
:scale: 30
:align: center
```

```{image} images/Picture74.svg
:scale: 30
:align: center
```

Видимо да је на позицију **2**, односно индекс 1, унет елемент који смо желели да
убацимо у низ.

```{questionnote}
Написати програм којим се уноси *n* елемената целобројног низа, затим
врши додавање жељеног елемента на одређеној позицији. Предвидети да, уколико
се унесе позиција која је ван опсега низа, програм испише поруку "Pozicija mora biti veca od nule i manja od broja elemenata niza." Уколико је све у реду, исписати проширени низ.
```
**Решење**:

```c
#include <stdio.h> 
int main(void)
{
    int i, j, a[50], n, k;
    printf("Koliko elemenata ima niz? ");
    scanf("%d", &n);
    printf("Unesi elemente niza: \n");
    for (i = 0; i < n; i++)
    {
        printf("a[%d] = ", i);
        scanf("%d", &a[i]);
	}
    printf("Unesi poziciju: ");
    scanf("%d", &j);
    if (j >= 0 && j <= n)
    {
        printf("Unesi element koji umeces: ");
        scanf("%d", &k);
        for (i = n; i > j - 1; i--)
            a[i] = a[i - 1];
        a[j - 1] = k;
        printf("\nProsireni niz izgleda ovako:\n");
        for (i = 0; i < n + 1; i++)
            printf("a[%d] = %d\n", i, a[i]);
    }
    else
        printf("Pozicija mora biti veca od nule i manja od broja elemenata niza.");
}
```

Ако је унета позиција у опсегу, на излазу се добија:

```text
Koliko elemenata ima niz? 5
Unesi elemente niza:
a[0] = 1
a[1] = 2
a[2] = 3
a[3] = 4
a[4] = 5
Unesi poziciju: 5
Unesi element koji umeces: 3

Prosireni niz izgleda ovako:
a[0] = 1
a[1] = 2
a[2] = 3
a[3] = 4
a[4] = 3
a[5] = 5
```

Ако унета позиција није у опсегу, на излазу се добија:

```text
Koliko elemenata ima niz?  5
Unesi elemente niza:
a[0] = 1
a[1] = 2
a[2] = 3
a[3] = 4
a[4] = 5

Unesi poziciju: 0
Pozicija mora biti veca od nule i manja od broja elemenata niza.
```