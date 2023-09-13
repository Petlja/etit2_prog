# Сажимање низова

```{infonote}
Сажимање представља избацивање појединих чланова низа и формирање новог низа.
```

```{questionnote}
Иницијализујте један низ од шест целобројних елемената a[6] = {1, 5, 3, 2, 4, 6}.
Сажмите низ тако што ћете избацити елементе који имају вредност ``izbaci = 2``. На основу
циклуса за сажимање написати програм.
```

```c
for (int i = 0; i < n; i++)     // 1
    {
        if (a[i] != izbaci)     // 2
            a[k++] = a[i];      // obrati paznju na redosled izvrsavanja, a[k] = a[i], k = k + 1   
    }
	n = k;
```

**Решење**:

```c
int main(void)
{
    int a[6] = {1, 5, 3, 2, 4, 6}, i, j, izbaci, n, k = 0;
    printf("Uneti niz:\n");
    for (i = 0; i < 6; i++)
        printf("a[%d] = %d\n", i, a[i]);
    printf("\nUnesite elemenat koji izbacujete: ");
    scanf("%d", &izbaci);
    for (int i = 0; i < 6; i++)
    {
        if (a[i] != izbaci)
            a[k++] = a[i];
    }
    n = k;
    printf("\nSazet niz izgleda ovako:\n");
    for (j = 0; j < n; j++)
        printf("a[%d] = %d\n", j, a[j]);
    return 0;
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

Unesite elemenat koji izbacujete: 2

Sazet niz izgleda ovako:
a[0] = 1
a[1] = 5
a[2] = 3
a[3] = 4
a[4] = 6
```

Хајде да анализирамо шта се налази у циклусу означеним бројем **1**. Унели смо да
се избацује елемент ``izbaci =  2``.

```{image} images/Picture61.svg
:scale: 30
:align: center
```

Следећи корак - ``i = i + 1``

```{image} images/Picture62.svg
:scale: 30
:align: center
```

Следећи корак - ``i = i + 1``

```{image} images/Picture63.svg
:scale: 30
:align: center
```

Следећи корак - ``i = i + 1`` 

```{image} images/Picture64.svg
:scale: 30
:align: center
```

Следећи корак - ``i = i + 1``

```{image} images/Picture65.svg
:scale: 30
:align: center
```

Следећи корак - ``i = i + 1`` 

```{image} images/Picture66.svg
:scale: 30
:align: center
```

Следећи корак - ``i = i + 1 = 6``. *For* циклус је достигао граничну вредност и прекида се.

Пошто је  je ``n = k``, ``n = 5``  на крају је остао низ

```{image} images/Picture67.svg
:scale: 30
:align: center
```

```{questionnote}
Написати програм којим се уноси *n* елемената целобројног низа, а затим
врши избацивање жељеног елемента. Предвидети да уколико се унесе вредност која се
не налази у низу испише поруку "U nizu ne postoji element za izbacivanje". Уколико је
све у реду исписати сажети низ.
```
Решење:

```c
#include <stdio.h> 
int main(void)
{
    int i, a[50], n, izbaci, k = 0;
    printf("Koliko elemenata ima niz? ");
    scanf("%d", &n);
    printf("Unesi elemente niza: \n");
    for (i = 0; i < n; i++)
    {
        printf("a[%d] = ", i);
        scanf("%d", &a[i]);
    }
    printf("\nUnesi element koji zelis da izbacis: ");
    scanf("%d", &izbaci);
    for (int i = 0; i < n; i++)
    {
        if (a[i] != izbaci)
            a[k++] = a[i];
    }
    if (n == k)
    {
        printf("\nU nizu ne postoji element za izbacivanje.");
        printf("\nNiz je ostao nepromenjen.\n");
        for (i = 0; i < n; i++)
            printf("a[%d] = %d\n", i, a[i]);
    }
    else
    {
        n = k;
        printf("\nSazet niz izgleda ovako:\n");
        for (i = 0; i < n; i++)
            printf("a[%d] = %d\n", i, a[i]);
    }
```

Ако се тражени елементи налазе у низу на излазу се добија:

```text
Koliko elemenata ima niz? 6
Unesi elemente niza:
a[0] = 5
a[1] = 2
a[2] = 2
a[3] = 8
a[4] = 9
a[5] = 5

Unesi element koji zelis da izbacis: 5

Sazet niz izgleda ovako:
a[0] = 2
a[1] = 2
a[2] = 8
a[3] = 9
```

Ако се тражени елементи не налазе у низу на излазу се добија:

```text
Koliko elemenata ima niz? 6
Unesi elemente niza:
a[0] = 5
a[1] = 2
a[2] = 2
a[3] = 8
a[4] = 9
a[5] = 5

Unesi element koji zelis da izbacis: 1

U nizu ne postoji element za izbacivanje.
Niz je ostao nepromenjen.
a[0] = 5
a[1] = 2
a[2] = 2
a[3] = 8
a[4] = 9
a[5] = 5
```
