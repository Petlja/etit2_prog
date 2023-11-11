# Додавање чвора у једноструко спрегнуту листу на почетак листе

Да бисмо додали  чвор на почетак листе потребно је да резервишемо адресу за нови чвор. Након тога ћемо сачувати адресу првог чвора у променљиву `temp`.

Затим ћемо нови чвор поставити на прво место тако што ћемо у показивач `prvi` унети адресу новог чвора.
Након тога у поље за адресу новог чвора уписујемо сачувану адресу претходног првог чвора.

```{image} images/image12.png
:width: 650
:align: center
```

```c
Lista *prvi, *novi, *temp;
novi = (Lista*)(malloc(sizeof(Lista));
temp = prvi;
prvi = novi;
prvi -> sl_adresa = temp;
```

На овај начин се нови елемент нашао на првом месту, а претходни први је постао други.

```{image} images/image13.png
:width: 650
:align: center
```

```{questionnote}
Написати функцију за додавање елемента на почетак једноструко спрегнуте листе.
```

**Решење**:

```c
Lista *dodaj_prvi(Lista *p, int broj)
{
    Lista *novi, *temp;
    novi = (Lista*)malloc(sizeof(Lista));
    temp = p;
    p = novi;
    p -> podatak = broj;
    p -> sl_adresa = temp;
    return p;	
}
```
