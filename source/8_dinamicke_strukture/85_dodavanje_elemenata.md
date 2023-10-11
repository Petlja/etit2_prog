# Додавање елемената у једноструко спрегнуту листу

Да бисмо креирали листу, можемо формирати функцију која ће додати одједном све чворове листе као у претходним примерима, али можемо и написати функцију којом ћемо убацивати чвор по чвор.

```{questionnote}
Написати функцију за унос чвор по чвор у једноструко спрегнуту листу. 
```

```c
Lista *dodaj(Lista *p, int vrednost)
{
    Lista *tekuci;
    if (p == NULL) /* ako je postojeca lista prazna dodaje se novi cvor kao pocetni */
    {
        p = (Lista*)malloc(sizeof(Lista));/* kreiranje novog cvora */
        if (p == NULL)
        {
            printf("Doslo je do greske\n");
            return NULL;
        }
        /* novom cvoru se dodeljuje prosledjeni podatak */
        p -> podatak = vrednost;
        p -> sl_adresa = NULL;
    }
    else
    {
        tekuci = p;	/* prolazi se kroz postojecu listu da bi se dobio pokazivac na poslednji cvor */
        while (tekuci -> sl_adresa != NULL) 
            tekuci = tekuci -> sl_adresa;
    /* kreiranje novog cvora */
        tekuci -> sl_adresa = (Lista*)malloc(sizeof(Lista));
        if (tekuci -> sl_adresa == NULL)
        {
            printf("Pogresno\n");
            return NULL;
        }
    /* novom cvoru se dodeljuje prosledjeni podatak, a njegova adresa se upisuje kao link prethodnog cvora */
        tekuci = tekuci -> sl_adresa;
        tekuci -> podatak = vrednost;
        tekuci -> sl_adresa = NULL;
    }
    return (p);
}
```

Примећујете да је тип функције, као и повратна вредност, показивач на структуру. 

