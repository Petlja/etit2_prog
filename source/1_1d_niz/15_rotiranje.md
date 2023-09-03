# Ротирање низа

```{infonote}
Ротирање низа представља померање чланова низа за одређен број места улево или удесно.
```

```{questionnote}
Иницијализујте један низ од шест целобројних елемената a[6] = {1, 5, 3, 2, 4, 6}.
Ротирајте иницијализовани низ за два места улево. Написати код на основу циклуса датог испод.
```

```c
for (i = 0; i < mesto; i++)
    {
        temp = a[0];
        for (j = 1; j < n; j++)
            a[j - 1] = a[j];
        a[n - 1] = temp;
    }
```

**Решење**:

```c
#include <stdio.h> 
main() 
{
#include <stdio.h> 
int main(void)
{
    int a[6] = {1, 5, 3, 2, 4, 6}, i, j, temp, mesto;
    printf("Uneti niz:\n");
    for (i = 0; i < 6; i++)
        printf("a[%d] = %d	", i, a[i]);
    printf("\nUnesite broj mesta za pomeranja niza: ");
    scanf("%d", &mesto);
    for (i = 0; i < mesto; i++)
    {
        temp = a[0];
        for (j = 1; j < 6; j++)
            a[j - 1] = a[j];
        a[6 - 1] = temp;
    }
    printf("\nUneti niz rotiran za %d mesta ulevo izgleda ovako:\n", mesto);
    for (j = 0; j < 6; j++)
        printf("a[%d] = %d	", j, a[j]);
    return(0);
}
```

**Излаз**:

```text
Uneti niz:
a[0]=1	a[1]=5	a[2]=3	a[3]=2	a[4]=4	a[5]=6

Unesite broj mesta za pomeranja niza: 2

Uneti niz rotiran za 2 mesta ulevo izgleda ovako:
a[0]=3	a[1]=2	a[2]=4	a[3]=6	a[4]=1	a[5]=5
```

Хајде да анализирамо корак по корак шта се дешава кроз циклус.


```c
for (i = 0; i < mesto; i++)
    {
        temp = a[0];
        for (j = 1; j < n; j++)
            a[j - 1] = a[j];
        a[n - 1] = temp;
    }
```

```{image} images/Picture52.png
:width: 70%
:align: center
```

```{image} images/Picture53.png
:width: 70%
:align: center
```

```{image} images/Picture54.png
:width: 70%
:align: center
```

```{image} images/Picture55.png
:width: 70%
:align: center
```

```{image} images/Picture56.png
:width: 70%
:align: center
```

```{image} images/Picture57.png
:width: 35%
:align: center
```

Пробај да направиш још један пролаз на идентичан начин почевши од

```{image} images/Picture58.png
:width: 70%
:align: center
```

Настави анализу до краја као предходно треба на крају да добијеш низ где
су елементи ротира за два места улево у односу на почетну позицију

```{image} images/Picture59.png
:width: 35%
:align: center
```

```{questionnote}
Написати програм којим се уноси n елемената целобројног низа, затим
врши ротирање и на крају исписује ротирани низ.
```

**Решење**:

```c
#include <stdio.h> 
int main(void)
{
    int i, j, a[50], n, temp, mesto;
    printf("Koliko elemenata ima niz? ");
    scanf("%d", &n);
    printf("\nUnesi elemente niza:\n");
    for (i = 0; i < n; i++)
    {
        printf("a[%d] = ", i);
        scanf("%d", &a[i]);
    }
    printf("\nUneti niz:\n");
    for (i = 0; i < n; i++)
        printf("a[%d] = %d   ", i, a[i]);
    printf("\n\nUnesi broj mesta za pomeranja niza: ");
    scanf("%d", &mesto);
    for (i = 0; i < mesto; i++)
    {
        temp = a[0];
        for (j = 1; j < n; j++)
            a[j - 1] = a[j];
        a[n - 1] = temp;
    }
    printf("\nUneti niz rotiran za %d mesta ulevo izgleda ovako:\n", mesto);
    for (j = 0; j < n; j++)
        printf("a[%d] = %d   ", j, a[j]);
    return(0);
}
```

**Излаз**:

```text
Koliko elemenata ima niz? 5

Unesi elemente niza:
a[0]=1
a[1]=2
a[2]=3
a[3]=4
a[4]=5

Uneti niz:
a[0]=1	a[1]=2	a[2]=3	a[3]=4	a[4]=5

Unesi broj mesta za pomeranja niza: 3

Uneti niz rotiran za 3 mesta ulevo izgleda ovako:
a[0]=4	a[1]=5	a[2]=1	a[3]=2	a[4]=3
```