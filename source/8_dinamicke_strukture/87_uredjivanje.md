# Уређивање једноструко спрегнуте листе

Уређивање садржаја листе може се радити на два начина:

- премештањем садржаја чворова (слично уређивању низова) и
- превезивањем чворова.

Најједноставније је премештање садржаја чворова. У примеру ћемо применити методу избора. Разлика је у томе што се уместо целобројних индекса користе показивачи на чворове.

```{questionnote}
Написати функцију за уређивање листе у опадајућем редоследу методом избора.
```

**Решење**:

```c
void sortiraj(Lista *p) 
{
    Lista *i, *j;
    int temp;
    for (i = p; i != NULL; i = i -> sl_adresa)
        for (j = p; j!= NULL; j = j -> sl_adresa)
            if (j -> podatak < i -> podatak) 
            {
                temp = i -> podatak;
                i -> podatak = j-> podatak;
                j -> podatak = temp;
            }	
}
```

```{questionnote}
Написати програм за унос, сортирање и испис једноструко спрегнуте листе од n целих бројева.
```

**Решење**:

```c
#include<stdio.h> 
#include<malloc.h> 
typedef struct lista 
{ 
    int podatak; 
    struct lista  *sl_adresa; 
} Lista;
Lista *unos(int n);
void ispis(Lista *p);
void sortiraj(Lista *p); 
main() 
{
    Lista *prvi, *novi;
    int n; 
    novi = (Lista*)malloc(sizeof(Lista));
    printf("Unesi broj elemenata: ");
    scanf("%d", &n);
    prvi = NULL; 
    prvi = unos(n);
    printf("\nLista pre sortiranja\n");
    ispis(prvi);
    sortiraj(prvi);
    printf("\nLista posle sortiranja\n");
    ispis(prvi);
}
```

**Излаз**:

```text
Unesi broj elemenata: 6
Unesi vrednost: -5
Unesi vrednost: 8
Unesi vrednost: 9
Unesi vrednost: 1
Unesi vrednost: -4
Unesi vrednost: 3

Lista pre sortiranja
-5      8       9       1       -4      3
Lista posle sortiranja
9       8       3       1       -4      -5
```
