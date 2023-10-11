# Проласци кроз једноструко спрегнуту листу

У раду са једноструко спрегнутим листама често је потребно кретати се кроз листу, од елемента до елемента. 

Најчешће је у питању обрада података у листи, претрага листе како би се нашао одговарајући елемент или тражење краја листе. У свим овим проласцима уводимо помоћни показивач tekuci и њему додељујемо вредност на први чвор листе коју уносимо споља, односно вредност адресе која је додељена првом чвору.
 
 ```c
void ispis(struct lista *p)
{
    struct lista *tekuci;
    tekuci = p;
    printf("Uneli ste listu\n");
    while (tekuci != NULL)
    {
        printf("%d\t", tekuci -> podatak);
        tekuci = tekuci -> sl_adresa;
    }
}
``` 

Након тога проверавамо да ли показивач показује на неки елемент (има вредност различиту од `NULL`) и врши се обрада податка у том елементу (испис, упоређивање, израчунавање...). По завршетку обраде податка, помоћни показивач `tekuci` добија вредност показивача на следећи елемент, а читав поступак се понавља све док помоћни показивач `tekuci` има вредност различиту од `NULL`, тј. док показује на неки чвор. Када помоћни показивач `tekuci` добије вредност `NULL`, то значи да смо дошли до краја листе.


```{questionnote}
Написати програм за унос `n` елемената једноструко спрегнуте листе целих бројева и израчунавање и испис збира и средње вредности елемената. Користити претходно дефинисану функцију за унос листе.
```

**Решење**:

```c
#include <stdio.h> 
#include <malloc.h> 
typedef struct lista  
{ 
    int podatak; 
    struct lista *sl_adresa; 
} Lista;

Lista *unos(int n); //funkcija za unos liste

int main(void) 
{
    //Unos elemenata liste 
    Lista  *prvi; 
    int n, i; 
    printf("Unesi broj elemenata: ");
    scanf("%d", &n);
    prvi = unos(n); //poziv funkcije za unos liste
    // Pristup elementima liste
    Lista *tekuci;
    tekuci = prvi;
    i = 0;
    int s = 0;
    while (tekuci != NULL)
    {
        s = s + tekuci -> podatak;
        i++;
        tekuci = tekuci -> sl_adresa;
    }
    printf("Zbir elemenata liste je %d\n", s);
    printf("Srednja vrednost elemenata liste je %.2f", (float)s / i);
    return 0;
}
```

**Излаз**:

```text
Unesi broj elemenata: 4
Unesi vrednost: 5
Unesi vrednost: 6
Unesi vrednost: 2
Unesi vrednost: 3
Zbir elemenata liste je 16
Srednja vrednost elemenata liste je 4.00
```

```{questionnote}
Написати функцију за пребројавање елемената листе.
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
```