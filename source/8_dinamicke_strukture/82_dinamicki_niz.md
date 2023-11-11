# Динамички низ

Као што смо раније рекли, приликом дефинисања низа морали смо унапред да дефинишемо простор који ћемо резервисати за низ. Употребом динамичких података то више није неопходно. Анализирајмо један пример дефинисања динамичког низа преко динамичких података.

**Пример**:

```c
#include <stdio.h>
#include <malloc.h>
int main(void)
{
    int *pa, n, i, s;
    printf ("Unesi broj elemenata: ");
    scanf("%d", &n);
    pa = (int*)malloc(n*sizeof(int));
    printf("Unesi elemente:\n");
    for (i = 0 ; i < n; scanf("%d", &pa[i++]));
    for (s = i = 0;i < n; s+ = pa[i++]);
    printf("\nZbir elemenata niza je %d\n", s);
    free(pa);
    return 0;
} 
```

**Излаз**:
```text
Unesi broj elemenata: 4
Unesi elemente:
2
4
5
7

Zbir elemenata niza je 18
```

Видимо да се не резервише простор за тачно одређен број елемената низа као кад га дефинишемо као статичку променљиву. 

У овом случају резервишемо на адреси pa меморијски простор за `n` елемената типа `int`.
Количина меморије која ће бити одвојена за низ зависи од броја елемената и типа података у низу. 