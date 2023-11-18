# Једноструко спрегнуте листе

Као што смо нагласили, чланови структуре могу бити и друге структуре али не и сама та структура. Међутим, њен члан може бити показивач на ту структуру. Захваљујући тој чињеници дефинишемо **листе**.

Листе су динамичке структуре података. Разликујемо једноструко спрегнуте и двоструко спрегнуте листе. Чланови структуре могу бити и друге структуре. 

Једна од веома честих примена динамичких структура је једноструко спрегнута листа.

```{infonote}
Једноструко спрегнута листа је скуп компоненти који се називају чворови (*node*). Сваки чвор (изузев последњег) садржи адресу наредног чвора. 
```

Због тога сваки чвор у једноструко спрегнутој линеарној листи има бар два елемента: један који садржи податке (*data*) и један који садржи адресу наредног чвора (*link*).

Података може бити више, као и адреса, али овде ћемо разматрати најједноставнији облик са једним податком и једном адресом. 

Дефинишимо чвор листе `lista` преко структуре...

```c
struct lista 
{
    int podatak;
    struct lista *sl_adresa;
};
```

... или структурног типа:

```c
typedef struct lista 
{
    int podatak;
    struct lista *sl_adresa;
} Lista;
```

Приметићете да при дефинисању структурног типа, мора да се наведе назив структуре без обзира на то што смо навели структурни тип, што није био случај када смо дефинисали обичну структуру. Ако то не урадимо, компајлер неће изјавити грешку, али ће дати упозорење.

```{image} images/image1.png
:width: 220
:align: center
```

Адреса првог чвора у листи се чува на посебној локацији коју ћемо звати глава листе (*head*), а у имплементацији ћемо је чувати у промењивој `prvi`. Адресу првог чвора, као и наредних, резервишемо наредбом `malloc`. 

```{image} images/image2.png
:width: 320
:align: center
```

Потребно је дефинисати променљиву `prvi`...

```c
struct lista *prvi; 
```

... или...

```c
Lista * prvi;
```

... која ће указивати на први чвор, односно на структуру којом је описан први податак који се налази на адреси `prvi`. 
Једноструко спрегнута листа је листа која се састоји од чворова, а редослед чворова у листи одређен је адресом која је записана у сваком чвору. На следећој слици приказан је пример једне једноструко спрегнуте листе.

```{image} images/image3.png
:width: 700
:align: center
```

Адреса у последњем чвору `sl_adresa = NULL`, то значи да даље немамо елементе у листи.

Поставља се питање како можемо приступити податку у листи. Дефинисаћемо показивач који ће садржати адресе појединачних елемената у листи. Дефинишимо показивач чије име је `tekuci` и нека је његова почетна вредност иста као и вредност показивача `prvi`. 

```c
struct lista *tekuci;
tekuci = prvi;
```

Након ове наредбе и показивач `tekuci` указује на поље podatak у првом чвору.

```{image} images/image4.png
:width: 700
:align: center
```

Размотримо следећу наредбу:

```c
tekuci = tekuci -> sl_adresa;
```

Овом наредбом се чита адреса `sl_adresa`  из чвора 1 и уписује у показивач `tekuci` тако да сад `tekuc` указује на чвор 2 и његово поље `podatak`.

```{image} images/image5.png
:width: 700
:align: center
```

Када tekuci добије вредност `NULL` значи да смо стигли до адресе у последњем чвору, односно на крај листе. У показивачу `tekuci` на крају остаје адреса последњег чвора у листи.

```{questionnote}
Анализирати поступак којим се формира једноструко спрегнута листа података од `n` бројева типа `int`. 
```

Посматрајмо структурни тип:

```c
typedef struct lista 
{
    int podatak;
    struct lista *sl_adresa;
} Lista;
```

Да би формирали листу, прво иницијализујемо празну листу доделом...

```c
prvi = NULL;
```

... и дефинишемо показиваче типа `Lista`:

```c
Lista *novi, *prvi, *poslednji;
```

Уводи се променљива poslednji у којој можемо сачувати адресу последњег чвора, што може у неким случајевима да нам буде од користи.

Након тога, како би се креирао први чвор листе, неопходно је да се додели меморијски простор. Користећи `malloc` резервишемо меморијски простор за први чвор, адресу уписујемо у показивач prvi и исту вредност уписујемо у показивач `novi`. Сада и prvi и novi показују на први чвор.

```c
prvi = (Lista*)malloc(sizeof(Lista));
novi = prvi; 
```

```{image} images/image6.png
:width: 260
:align: center
```

Формираном чвору могу се доделити почетне вредности, нпр:

```c
novi -> podatak = 5;
novi -> sl_adresa = NULL;
poslednji -> sl_adresa = novi; 
poslednji = novi;
```

```{image} images/image7.png
:width: 310
:align: center
```
За додавање новог чвора у листу најпре се мора одвојити простор за нови чвор:

```c
novi = (Lista*)malloc(sizeof(Lista));
```

```{image} images/image8.png
:width: 460
:align: center
```

Новом чвору у листи можемо доделити нове вредности:

```c
novi -> broj = 10;
novi -> sl_adresa = NULL; 
poslednji -> sl_adresa = novi; 
poslednji = novi;
```

```{image} images/image9.png
:width: 460
:align: center
```

За додавање новог чвора у листу поново се мора одвојити простор за нови чвор:

```c
novi = (Lista*)malloc(sizeof(Lista)); 
```

```{image} images/image10.png
:width: 650
:align: center
```

Новом чвору у листи можемо доделити нове вредности:

```c
novi -> broj = 15;
novi -> sl_adresa = NULL;
poslednji -> sl_adresa = novi; 
poslednji = novi;
```

```{image} images/image11.png
:width: 650
:align: center
```

Напишимо кôд за ово изнад изложено.

```{questionnote}
Написати програм за унос и испис елемената једноструко спрегнуте листе
```

```c
#include <stdio.h> 
#include <malloc.h> 

typedef struct lista 
{ 
    int podatak; 
    struct lista  *sl_adresa; 
} Lista; 

int main(void) 
{
    //Unos elemenata liste 
    Lista  *prvi, *poslednji, *novi; 
    int a, n, i; 
    printf("Unesi broj elemenata: ");
    scanf("%d", &n);
    prvi = NULL; 
    poslednji = NULL; 
    novi = NULL; 
    for (i = 0; i < n; i++) 
    { 
        novi = (Lista*)malloc(sizeof(Lista)); 
        if (novi) // ako je dodeljen memorijski prostor  
        { 	
            printf("Unesi vrednost: ");
            scanf("%d", &a);
            novi -> podatak = a; 
            novi -> sl_adresa = NULL; 
        } 
        else 
            break; 
        if (prvi == NULL) //ako je lista prazna  
        { 
            prvi = novi; 
            poslednji = novi; 
        } 
        else 
        { 
            poslednji -> sl_adresa = novi; 
            poslednji = novi; 
        }    
    }
    // Prikaz elemenata liste
    Lista *tekuci;
    tekuci = prvi;
    i = 0;
    while (tekuci != NULL)
    {
        printf("Vrednost podatka u cvoru elementa %d je %d\n",i+1, tekuci -> podatak);
        printf("Adresa podatka u cvoru elementa %d liste je %d\n", i+1, &tekuci -> podatak);
        printf("Adresa narednog cvora u cvoru elementa %d liste je %d\n\n", i+1, tekuci -> sl_adresa);
        i++;
        tekuci = tekuci -> sl_adresa;
    } 
    return 0;
} 
```

**Излаз**:

```text
Unesi broj elemenata: 4
Unesi vrednost: 58
Unesi vrednost: 25
Unesi vrednost: 12
Unesi vrednost: 1
Vrednost podatka u cvoru elementa 1 je 58
Adresa podatka u cvoru elementa 1 liste je 7476256
Adresa narednog cvora u cvoru elementa 1 liste je 7476288

Vrednost podatka u cvoru elementa 2 je 25
Adresa podatka u cvoru elementa 2 liste je 7476288
Adresa narednog cvora u cvoru elementa 2 liste je 7476320

Vrednost podatka u cvoru elementa 3 je 12
Adresa podatka u cvoru elementa 3 liste je 7476320
Adresa narednog cvora u cvoru elementa 3 liste je 7476352

Vrednost podatka u cvoru elementa 4 je 1
Adresa podatka u cvoru elementa 4 liste je 7476352
Adresa narednog cvora u cvoru elementa 4 liste je 0
```

Ово је био пример додавања елемената листе на крај листе. У наредним примерима видећете као се елементи могу додавати на почетак исте.

С обзиром да су листе показивачке структуре, могу се користити у функцијама и такође могу бити повратна вредност функције. 

```{questionnote}
Написати програм за унос и испис елемената једноструко спрегнуте листе целих бројева. Користити функције. 
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

Lista *unos(int n)
{
    Lista  *prvi, *poslednji, *novi; 
    int a, i; 
    prvi = NULL; 
    poslednji = NULL; 
    novi = NULL; 
    for (i = 0; i < n; i++) 
    { 
        novi = (Lista*)malloc(sizeof(Lista)); 
        if (novi) // ako je dodeljen memorijski prostor  
        {
            printf("Unesi vrednost: ");
            scanf("%d", &a);
            novi -> podatak = a; 
            novi -> sl_adresa = NULL; 
        } 
        else 
            break; 
        if (prvi == NULL) //ako je lista prazna  
        { 
            prvi = novi; 
            poslednji = novi; 
        } 
        else 
        { 
            poslednji -> sl_adresa = novi; 
            poslednji = novi; 
        }    
    }
    return prvi;
}

void ispis(Lista *p)
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

int main(void) 
{
    int n; 
    Lista *p;
    printf("Koliko elemenata unosis? ");
    scanf("%d", &n);
    p = unos(n);//poziv funkcije za unos
    ispis(p);//poziv funkcije za ispis
    return 0;
}
```

**Излаз**:

```text
Koliko elemenata unosis? 5
Unesi vrednost: 1
Unesi vrednost: 2
Unesi vrednost: 3
Unesi vrednost: 4
Unesi vrednost: 5
Uneli ste listu
1       2       3       4       5
```

Основне операције са једноструко спрегнутом листом обухватају:

- Претраживање листе да би се приступило одговарајућем податку у листи (читање или писање)
- Уметање новог члана (чвора) листе
- Брисање постојећег (чвора)  члана листе

Све наведене операције захтевају „пролазак” кроз листу.
