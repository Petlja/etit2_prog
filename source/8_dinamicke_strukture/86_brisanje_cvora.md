# Брисање чвора из једноструко спрегнуте листе

Брисање подразумева уклањање чвора из листе и ослобађање заузете меморије.

## Брисање чвора из једноструко спрегнуте листе по позицији

Да бисмо обрисали одређени чвор из листе, потребно је да знамо његову позицију у листи. Најједноставнији начин је да знамо редни број чвора у листи, уз претпоставку да су чворови нумерисани редом од 1 до `n`. Кад знамо редни број чвора, крећемо се кроз листу како бисмо пронашли показивач на тражени чвор. Потребно је да знамо адресе траженог чвора, претходног и наредног. Претпоставимо да треба да обришемо чвор 2. То значи да у показивач `sl_adresa` чвора 1 треба уместо адресе чвора 2 уписати адресу чвора 3, а након тога ослободити меморијски простор који је заузимао чвор 2. 

```{image} images/image18.png
:width: 630
:align: center
```

Након брисања чвора 2 имамо листу:

```{image} images/image19.png
:width: 470
:align: center
```

```{questionnote}
Написати програм за унос `n` чворова листе, брисање чвора на позицији `p` и штампање листе пре и после брисања елемента. Користити функције за унос и испис листе.
```

**Решење**:

```c
#include <stdio.h> 
#include <malloc.h> 

typedef struct lista 
{ 
    int podatak; 
    struct lista  *sl_adresa; 
} Lista;

Lista *unos(int n); // Prototip funkcije za unos liste
void ispis(Lista *p); // Prototip funkcije za ispis liste

int main(void) 
{
    //Unos liste 
    Lista  *prvi, *tekuci; 
    int n ,i, p; 
    printf("Unesi broj elemenata ");
    scanf("%d", &n);
    prvi = unos(n);//Poziv funkcije za unos liste
    // Ispis liste
    printf("Lista pre brisanja\n");
    ispis(prvi); //Poziv funkcije za ispis liste
    //Brisanje cvora liste
    printf("\nUnesi redni broj cvora koji brises ");
    scanf("%d", &p);
    Lista *prethodni, *sledeci;
    prethodni = NULL;
    tekuci = prvi;
    i = 1;
    while (i < p)
    {
        prethodni = tekuci;
        tekuci = tekuci -> sl_adresa;
        i++;
    }
    if (prethodni == NULL)
    {
        prvi = tekuci -> sl_adresa;
        free(tekuci);
    }
    else
    {
        prethodni -> sl_adresa = tekuci -> sl_adresa;
        free(tekuci);
    }
    printf("Lista posle brisanja\n");
    ispis(prvi); //Poziv funkcije za ispis liste
    return 0;
}
```

**Излаз**:

```text
Unesi broj elemenata: 7
Unesi vrednost: 1
Unesi vrednost: 2
Unesi vrednost: 3
Unesi vrednost: 4
Unesi vrednost: 5
Unesi vrednost: 6
Unesi vrednost: 7
Lista pre brisanja
1       2       3       4       5       6       7
Unesi redni broj elementa koji brises 4
Lista posle brisanja
1       2       3       5       6       7
```


```{questionnote}
Написати функцију за брисање чвора на редном броју.
```

**Решење**:

```c
Lista *brisi(Lista *p, int k)
{
    int i;
    Lista *prethodni, *tekuci;
    prethodni = NULL;
    tekuci = p;
    i = 1;
    while ( i < k )//u tekuci se upisuje adresa cvora za brisanje
    {
        prethodni = tekuci;
        tekuci = tekuci -> sl_adresa;
        i = i + 1;
    }
    if (prethodni == NULL)
    {
        p = tekuci -> sl_adresa;
        free(tekuci);
    }
    else
    {
        prethodni -> sl_adresa = tekuci -> sl_adresa;
        free(tekuci);
    }
    return p;	
}
```

Иста функција може да се искористи да би се обрисао елемент одређене вредности. У циклусу за пролазак кроз матрицу циклус се прекида када се нађе податак задате вредности. Под условом да је нпр. тражена вредност `broj`, циклус `while` би био:
 

 ```c
while (tekuci -> podatak != broj)//u tekuci se upisuje adresa cvora za brisanje
    {
        prethodni = tekuci;
        tekuci = tekuci->sl_adresa;
    }
```

```{questionnote}
Написати функцију за брисање чвора који садржи тражену вредност.
```

**Решење**:


```c
Lista *brisi_vrednost(Lista *p, int broj)
{
    int i;
    Lista *prethodni, *tekuci;
    prethodni = NULL;
    tekuci = p;
    while (tekuci -> podatak != broj)//u tekuci se upisuje adresa cvora za brisanje
    {
        prethodni = tekuci;
        tekuci = tekuci -> sl_adresa;
    }
    if (prethodni == NULL)
    {
        p = tekuci -> sl_adresa;
        free(tekuci);
    }
    else
    {
        prethodni -> sl_adresa = tekuci -> sl_adresa;
        free(tekuci);
    }
    return p;	
}
```

## Брисање првог чвора једноструко спрегнуте листе

 Да бисмо обрисали први чвор из листе потребно је једноставно да у показивач `prvi` који показује на адресу првог чвора унесемо адресу другог чвора. Након тога ослобађамо меморијски простор који је заузимао чвор 1. 

```{image} images/image20.png
:width: 620
:align: center
``` 
Након брисања чвора имамо листу:

```{image} images/image21.png
:width: 470
:align: center
```

```{questionnote}
Написати функцију за брисање чвора на почетку једноструко спрегнуте листе.
```

**Решење**:

```c
Lista *brisi_prvi(Lista *p)
{
    Lista *tekuci;
    if (p == NULL)
        return;
    tekuci = p -> sl_adresa;
    free(p);
    p = tekuci;
    return p;	
}
```

## Брисање чвора на крају једноструко спрегнуте листе

Да бисмо обрисали последњи чвор из листе потребно је једноставно у поље претпоследњег чвора унети `NULL` и на тај начин завршити листу. Након тога ослобађамо меморијски простор који је заузимао чвор `n`. 

```{image} images/image21.png
:width: 540
:align: center
```

Након брисања чвора имамо листу:

```{image} images/image22.png
:width: 600
:align: center
```

```{questionnote}
Написати функцију за брисање чвора листе на крају листе. Користити функцију која одређује дужину листе.
```

**Решење**:

```c
int duzina(Lista *p)
{
    int broj = 0 ;
    while (p != NULL)
    {
        broj++;
        p = p -> sl_adresa;
    }
    return (broj);
}
Lista *brisi_poslednji(Lista *p)
{
    Lista *tekuci;
    int i;
    if (p == NULL)
    return NULL;
    tekuci = p;
    for (i = 0; i < duzina(p) - 2; i++)
        tekuci = tekuci -> sl_adresa;
    tekuci -> sl_adresa = NULL;
    return p;	
}
```

У овом случају морамо наћи адресу претпоследњег чвора и у његово поље резервисано за адресу наредног чвора уписати `NULL`. Адреса тог чвора налази се у чвору који му претходи. 

```{questionnote}
Написати функцију за брисање чвора на крају листе без функције која налази дужину листе.
```

**Решење**:

```c
Lista *brisi_poslednji(Lista *p)
{
    Lista *tekuci, *prethodni;
    if (p == NULL)
        return NULL;
    tekuci = p;
    prethodni = p;
    while (tekuci -> sl_adresa != NULL)
    {
        prethodni = tekuci;
        tekuci = tekuci -> sl_adresa;
    }
    prethodni -> sl_adresa = NULL;
    free(tekuci);
    return p;	
}
```

## Брисање целе једноструко спрегнуте листе 

Код брисања целе листе у `tekuci` се учитава адреса почетка листе, односно првог чвора, а почетак листе се помера на адресу наредног. Поступак се понавља све док се не дође до краја листе, односно док `tekuci` не добије вредност `NULL`.

```c
void brisi(Lista *p) 
{
    Lista *tekuci=NULL;
    while (p!=NULL) 
    {
        tekuci = p -> sl_adresa;
        free(tekuci);
        p = tekuci; 
    }
}
```
