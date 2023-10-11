# Додавање чвора унутар једноструко спрегнуте листе

Да бисмо додали елемент на одређени индекс у листи, потребно је одрадити неколико корака:
- да резервишемо меморијски простор за чвор,
- да пронађемо адресу чвор пре индекса на који се уноси нови чвор,
- да пронађемо адресу чвор после индекса на који се уноси нови чвор.

```{image} images/image16.png
:width: 680
:align: center
```

Након тога се у чвор на позицији `i - 1` уписује адреса новог чвора, а онда се у нови чвор уписује податак и адреса чвора на позицију индекс `i + 1`.

```{image} images/image17.png
:width: 680
:align: center
```

```{questionnote}
Написати функцију за додавање чвора на одређени индекс у једноструко спрегнутој листи. 
```

**Решење**:

```c
Lista *dodaj_na_indeks(Lista *p, Lista *novi, int index)
{
    int i;
    if (p == NULL)
        {
            novi-> sl_adresa = NULL;
            p = novi;
            return p;
        }
    Lista *tekuci = p;
    if (index == 0)
    {
        novi -> sl_adresa = p;
        p = novi;
        return p;
    }
    for (i = 0; tekuci -> sl_adresa != NULL; i++, tekuci = tekuci -> sl_adresa)
        if (i == index - 1)
            break;
    novi -> sl_adresa = tekuci -> sl_adresa;
    tekuci -> sl_adresa = novi;
    return p;
}
```