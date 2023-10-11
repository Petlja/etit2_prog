# Додавање чвора у једноструко спрегнуту листу на крај листе

Да бисмо додали  чвор на крај листе потребно је да резервишемо адресу за нови чвор. 
Затим ћемо у нови чвор проследити вредност за податак и у поље за адресу унети `NULL`, што значи да је он последњи у листи.

Након тога ћемо пронаћи адресу последњег чвора и уписати је у променљиву `poslednji`.
На крају ћемо у чвор на који показује `poslednji` у поље за адресу унети novi, односно адресу новог чвора.

```{image} images/image14.png
:width: 680
:align: center
```

```c
Lista *novi, *tekuci, *poslednji;
novi = (Lista*)(malloc(sizeof(Lista))
novi -> sl_adresa = NULL;
poslednji = novi;
poslednji -> sl_adresa = novi;
```

На овај начин се нови елемент нашао на последњем месту: 

```{image} images/image15.png
:width: 720
:align: center
```

```{questionnote}
Написати функцију за додавање чвора на крај листе.
```

**Решење**:

```c
Lista *dodaj_zadnji(Lista *p, int broj)
{
    Lista *novi, *tekuci, *poslednji;
    novi = (Lista*)malloc(sizeof(Lista));
    novi -> podatak = broj;
    novi -> sl_adresa = NULL;
    tekuci = p;
    while (tekuci -> sl_adresa != NULL)
        tekuci = tekuci -> sl_adresa;
    poslednji = tekuci;
    poslednji -> sl_adresa = novi;
    return p;
}
```