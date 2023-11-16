# Инвертовање низова

```{infonote}
Инвертовање представља замену чланова низа тако да први постане задњи, други предзадњи и тако редом.  
```

Постоје два начина на које се инвертовање низа може постићи:

- уз увођење новог низа
- без увођења новог низа

Погледајмо како изгледа циклус за инвертовање увођењем новог низа

```c
for (i = 0; i < n; i++)
    b[n-1-i] = a[i]
```

```{questionnote}
Иницијализујте један низ од шест целобројних елемената a[6] = {1, 5, 3, 2, 4, 6}.
Напишите програм за инвертовање низа уз увођење новог низа користећи претходни циклус.
```

**Решење**:

```c
#include <stdio.h> 
int main(void)
{
    int a[6] = {1, 5, 3, 2, 4, 6}, b[6], i, j;
    printf("Uneti niz:\n");
    for (i = 0; i < 6; i++)
        printf("a[%d] = %d\n", i, a[i]);
    for (i = 0; i < 6; i++)
        b[5 - i] = a[i];
    printf("\nInvertovani niz:\n");
    for (i = 0; i < 6; i++)
       printf("a[%d] = %d\n", i, b[i]);
    return 0;
}
```

У овом случају ћемо један по један елемент из низа а уносити у низ ``b``. Први
члан низа ``а`` пресликавамо у последњи низа ``b``. Други члан низа ``а`` пресликавамо
у претпоследњи низа ``b``. И тако редом.

Хајде да анализирамо корак по корак шта се дешава кроз циклус.

```{image} images/Picture45.svg
:scale: 30
:align: center
```

```{image} images/Picture46.svg
:scale: 30
:align: center
```

```{image} images/Picture47.svg
:scale: 30
:align: center
```

```{image} images/Picture48.svg
:scale: 30
:align: center
```

```{image} images/Picture49.svg
:scale: 30
:align: center
```

```{image} images/Picture50.svg
:scale: 30
:align: center
```
Погледајмо како изгледа циклус за инвертовање без увођења новог низа

```c
for (i = 0, ј = n - 1; i < j; i++, j--)
    {
        b = a[i];
        a[i] = a[ј];
        a[j] = b;
    }
```

```{questionnote}
Иницијализујте један низ од шест целобројних елемената a[6] = {1, 5, 3, 2, 4, 6}.
На основу претходног циклуса написати програм за инвертовање.
```

**Решење**:

```c
#include <stdio.h> 
int main(void)
{
    int a[6] = { 1, 5, 3, 2, 4, 6}, b, i, j;
    printf("Uneti niz:\n");
    for (i = 0; i < 6; i++)
        printf("a[%d] = %d\n", i, a[i]);
    for (i = 0, j = 5; i < j; i++, j--)
    {
        b = a[i]; 
        a[i] = a[j]; 
        a[j] = b;
    }
    printf("\nInvertovani niz:\n");
    for (i = 0; i < 6; i++)
        printf("a[%d] = %d\n", i, a[i]);
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

Invertovani niz:
a[0] = 6
a[1] = 4
a[2] = 2
a[3] = 3
a[4] = 5
a[5] = 1
```
Добија се идентичан излаз као са увођењем новог низа.

Хајде да анализирамо корак по корак шта се дешава кроз циклус

Променљива ``b`` нам служи да привремено сачувамо вредност низа коју
замењујемо другом вредношћу.

```{image} images/Picture41.svg
:scale: 30
:align: center
```

```{image} images/Picture42.svg
:scale: 30
:align: center
```

```{image} images/Picture43.svg
:scale: 30
:align: center
```

Приметићете да у овом случају нисмо уводили нови низ.


```{questionnote}
Написати програм којим се уноси n елемената целобројног низа,
а затим се врши инвертовање унетог низа на оба начина. Исписати инвертоване
низове.
```

**Решење без увођења новог низа**:

```c
#include <stdio.h> 
int main(void)
{
    int b, i, j, a[50], n;
    printf("Koliko elemenata ima niz? ");
    scanf("%d", &n);
    printf("Unesi elemente niza:\n");
    for (i = 0; i < n; i++)
    {
        printf("a[%d] = ", i);
        scanf("%d", &a[i]);
    }
    printf("\nUneti niz:\n");
    for (i = 0; i < n; i++)
        printf("a[%d] = %d\n", i, a[i]);
    for (i = 0, j = n - 1; i < j; i++, j--)
    {
        b = a[i];
        a[i] = a[j];
        a[j] = b;
    }
    printf("\nInvertovani niz:\n");
    for (i = 0; i < n; i++)
        printf("a[%d] = %d\n", i, a[i]);
    return 0;
}
```

**Решење са увођењем новог низа**:

```c
#include <stdio.h> 
int main(void)
{
    int i, j, a[50], b[50], n;
    printf("Koliko elemenata ima niz? ");
    scanf("%d", &n);
    printf("Unesi elemente niza:\n");
    for (i = 0; i < n; i++)
    {
        printf("a[%d] = ", i);
        scanf("%d", &a[i]);
    }
    for (i = 0; i < n; i++)
        b[n - i] = a[i];
    printf("\nInvertovani niz:\n");
    for (i = 0; i < n; i++)
        printf("a[%d] = %d\n", i, a[i]);
    return 0;
}
```

**Излаз**:

```text
Koliko elemenata ima niz? 5
Unesi elemente niza:
a[0] = 1
a[1] = 2
a[2] = 3
a[3] = 4
a[4] = 5

Invertovani niz:
a[0] = 5
a[1] = 4
a[2] = 3
a[3] = 2
a[4] = 1
```
