# Претраживање низова

Имамо низ и желимо да видимо да ли се у њему налази неки елемент. Шта ћемо
урадити? Најједноставнији начин је да упоређујемо вредност траженог елемента са
сваким појединачним елементом у низу.

```{questionnote}
Шта ако...
- не постоји елемент у низу?
- имамо два или више иста елемената у низу?
- имамо низ са огромним бројем елемената?
- низ није уређен?
```


```{infonote}
- Задатак претраживања је проналажење елемента низа који задовољава неки унапред задат услов.
- Претраживањем се утврђује да ли задати елеменат постоји у низу вредности и ако постоји који је његов индекс односно позиција.
- Најбоље претраживање је оно које има најмањи број поређења које је потребно извести у поступку тражења задатих вредности.
```

Разликујемо две врсте претраживања којима ћемо се бавити:

- секвенцијално претраживање
- бинарно претраживање

Кренимо редом.

## Секвенцијално претраживање

Присетимо се како су некада ваши родитељи слушали музику. Имали су уређај који се звао
вокмен и који је користио касете. На њима су се налазиле снимљене песме. На касети је
могло бити снимљено више десетина песама. Сретну друга и кажу: „Дај, пусти ми ону...“

Шта онда? Песма је могла бити прва по реду, а могла је бити и последња. Значи, пуштали би
једну по једну док не би нашли „ону праву“.

Или, рецимо, давно заборављени грамофон.

Уколико имамо списак песама, као код грамофонских плоча, није проблем – тачно знамо на којој
је позицији, односно индексу. А шта ако немамо списак? Поново морамо пуштати једну по једну,
док не нађемо жељену песму.

Исти случај је код низова.

Низ може бити уређен или неуређен. У низу не мора да постоји тражени елемент, али може да их
постоји и више. Много питања, хајде да дамо одговоре.

Секвенцијално претраживање неуређеног низа

Дефинисали смо један неуређени низ a од n елемената:

```{image} images/Picture1.png
:width: 50%
:align: center
```

Претпоставимо да тражимо елемент ``t`` који има одређену вредност. Да пробамо да направимо циклус
који ће приступити сваком елементу и проверити да ли има вредност ``t``.

Шта може да се утврди? Најједноставније је да се одреди индекс на коме се налази та вредност.

```{questionnote}
A шта ако у низу не постоји та вредност?
```

Управо из тог разлога уводимо променљиву ``indeks`` и додељујемо јој почетну вредност -1. Уколико
нађемо елемент, променљива ``indeks`` добија вредност индекса тог елемента. У супротном, вредност
``indeks`` ће остати -1, што значи да елемент није пронађен у низу.

Овај начин размишљања се користи у већини програмских језика.

Напишите следећи кôд и пробајте да схватите шта он ради.

```c
#include <stdio.h> 
int main(void)
{
    int a[100], n, t, i, indeks = -1;
    printf("Koliko elemenata ima niz? ");
    scanf("%d", &n);
    printf("Unesi elemente niza:\n");
    for (i = 0; i <= n - 1; i++)
    {
        printf("a[%d] = ", i);
        scanf("%d", &a[i]);
    }
    printf("Unesi element koji trazis: ");
    scanf("%d", &t);
    for (i = 0; i < n; i++)
    {
        if (a[i] == t)
            indeks = i;
    }
    if (indeks == -1)
        printf("\nU nizu ne postoji trazeni element.");
    else
        printf("\nPronadjen je element na %d. mestu, odnosno sa indeksom %d.", indeks + 1, indeks);
    return(0);
}
```

Први циклус служи да се унесу елементи низа, док се другим циклусом приступа сваком
елементу низа и проверава се да ли је елемент једнак траженој вредности. Уколико јесте,
променљива ``indeks`` добија вредност индекса елемента који је једнак траженој вредности. 

Ако ниједан елемент није једнак траженој вредности, ``indeks`` остаје -1 и то ћемо искористити
у последњем ``if else`` услову.

Ако се тражена вредност налази у низу, добићемо на излазу:

**Излаз**:

```text
Koliko elemenata ima niz? 5
Unesi elemente niza:
a[0] = 5
a[1] = 1
a[2] = 2
a[3] = 2
a[4] = 3
Unesi element koji trazis: 2

Pronadjen je element na 4. mestu, odnosno sa indeksom 3.
```

Приметићете да се упоређивање не прекида када се пронађе први индекс који задовољава
услов већ се претраживање наставља до краја.

Да видимо шта се дешава ако се тражена вредност не налази у низу.

**Излаз**:

```text
Koliko elemenata ima niz? 5
Unesi elemente niza:
a[0] = 5
a[1] = 1
a[2] = 2
a[3] = 2
a[4] = 3
Unesi element koji trazis: 6

U nizu ne postoji trazeni element.
```
```{questionnote}
Промени део кода тако да програм пребројава колико има тражених елемената у низу.
```

**Решење**:

```c
#include <stdio.h> 
int main(void)
{
    int a[100], n, t, i, indeks = -1, br = 0;
    printf("Koliko elemenata ima niz? ");
    scanf("%d", &n);
    printf("Unesi elemente niza:\n");
    for (i = 0; i <= n - 1; i++)
    {
        printf("a[%d] = ", i);
        scanf("%d", &a[i]);
    }
    printf("Unesi element koji trazis: ");
    scanf("%d", &t);
    for (i = 0; i < n; i++)
    {
        if (a[i] == t)
        {
            indeks = i;
            br++;
        }
    }
    if (indeks == -1)
        printf("U nizu ne postoji trazeni element.");
    else
        printf("\nPronadjeno je %d elemenata, a poslednji je %d. mestu, odnosno sa indeksom %d.", br, indeks + 1, indeks);
return(0);
}
```

**Излаз**:

```text
Koliko elemenata ima niz? 5
Unesi elemente niza:
a[0] = 5
a[1] = 1
a[2] = 2
a[3] = 2
a[4] = 3
Unesi element koji trazis: 2

Pronadjeno je 2 elemenata, a poslednji je na 4. mestu, odnosno sa indeksom 3.
```

Ово је био пример једног неуређеног низа.

## Секвенцијално претраживање уређеног низа

Посматрајмо један уређен низ.

```{image} images/Picture2.png
:width: 50%
:align: center
```

Напишите кôд као у претходном случају, али га промените тако да се извршавање прекида
када се пронађе тражени елемент.

```c
#include <stdio.h> 
int main(void)
{
    int a[100], n, t, i, indeks = -1;
    printf("Koliko elemenata ima niz? ");
    scanf("%d", &n);
    printf("Unesi elemente niza:\n");
    for (i = 0; i <= n - 1; i++)
    {
        printf("a[%d] = ", i);
        scanf("%d", &a[i]);
    }
    printf("Unesi element koji trazis: ");
    scanf("%d", &t);
    for (i = 0; i < n; i++)
    {
        if (a[i] == t)
        {
            indeks = i;
            break;
        }
    }
    if (indeks == -1)
        printf("\nU nizu ne postoji trazeni element.");
    else
        printf("\nPronadjen je element na %d. mestu, odnosno sa indeksom %d.", indeks + 1, indeks);
    return(0);
}
```

Примећујемо да смо циклус за упоређивање променили тако што смо додали наредбу
break када се пронађе тражена вредност.

Ако се тражена вредност налази у низу, добићемо на излазу:

**Излаз**:

```text
Koliko elemenata ima niz? 5
Unesi elemente niza:
a[0] = 1
a[1] = 2
a[2] = 2
a[3] = 3
a[4] = 8
Unesi element koji trazis: 2

Pronadjen je element na 2. mestu, odnosno sa indeksom 1.
```
```{mchoice}
:answer1: Може.
:answer2: Не може.
:correct: 1

Да ли се ова претрага може урадити помоћу *while* или *do while* циклуса? 
```

Код за претраживање:

```c
#include <stdio.h> 
int main(void)
{
    int a[100], n, t, i, indeks = -1;
    printf("Koliko elemenata ima niz?");
    scanf("%d", &n);
    printf("Unesi elemente niza:\n");
    for (i = 0; i < n; i++)
    {
        printf("a[%d] = ", i);
        scanf("%d", &a[i]);
    }
    printf("Unesi element koji trazis: ");
    scanf("%d", &t);
    i = 0;
    do
    {
        if (a[i] == t)
            indeks = i;
        i++;
    } while (i < n && indeks < 0);
    if (indeks == -1)
        printf("\nU nizu ne postoji trazeni element.");
    else
        printf("\nPronadjen je element na %d. mestu, odnosno sa indeksom %d.", indeks + 1, indeks);
    return(0);
}
```

На излазу као и у претходном случају добијамо редни број односно индекс првог пронађеног елемента у низу.

**Излаз**:

```text
Koliko elemenata ima niz? 5
Unesi elemente niza:
a[0] = 1
a[1] = 2
a[2] = 2
a[3] = 3
a[4] = 8
Unesi element koji trazis: 2

Pronadjen je element na 2. mestu, odnosno sa indeksom 1.
```

У случају да не постоји елемент, добићемо одговор да "U nizu ne postoji trazeni element."

```{infonote}
Секвенцијално претраживање можемо користити када број елемената низа није велики.
```

## Бинарно претраживање

Шта можемо да урадимо када имамо огроман број елемената нпр. милион или милијарду.
Секвенцијалним начином то може да потраје.

На пример, имамо сто хиљада елемената и баш је сто хиљадити онај који тражимо. То значи сто хиљада
упоређивања, а то траје.

Хајде да размислимо. Посматрајмо један уређени целобројни низ:

a[10]={1, 2, 3, 4, 5, 6, 7, 8, 9, 10}. Тражимо на пример вредност ``t = 2``.

```{image} images/Picture3.png
:width: 50%
:align: center
```

Да пробамо. Поделимо низ на пола и проверимо да ли је тражена вредност ``t`` баш једнака
тој вредности елемента низа са индексом који се налази у средини низа.

Тражимо индекс елемента који се налази у средини низа ``srednji``.

``srednji`` је индекс елемента у средини, ``donji`` је индекс првог елемента низа, а ``gornji`` је
индекс последњег елемента у низу.

Рачунамо $srednji= \frac{donji + gornji} {2}$. У нашем случају $srednji = \frac{0 + 9} {2}$.

С обзиром да је у питању целобројно дељење индекс елемента на средини је ``srednji = 4``.

```{image} images/Picture4.png
:width: 50%
:align: center
```

Ако је тражена вредност ``t`` једнака вредности елемента на том индексу одлично прекидамо
претраживање и тражени индекс је баш тај.

А шта ако није?

Проверавамо да ли је ``a[srednji] == t``. У нашем случају видимо да то није тачно па настављамо даље.

Пошто је низ уређен тражени елемент се налази или лево или десно од средине. Проверавамо да ли
се тражени елемент већи или мањи од елемента у средини.

Ако је низ растући и ако је ``a[srednji] > t`` то значи да се елемент налази са леве стране средњег
елемента. У супротном он се налази са десне стране.

Код нас је ``a[srednji] > t``. Сада одбацујемо све елементе са десне стране, јер знамо да се тражени
елемент налази лево од средине.

Преостали низ поново делимо на пола. Сада је ``donji = 0``, ``gornji = srednji - 1 = 3``.

Рачунамо $srednji = \frac{donji+gornji} {2}$.  У нашем случају $srednji = \frac{0+3} {2}$. Као и  у предходном
случају, у питању целобројно дељење и индекс елемента на средини је ``srednji = 1``.

```{image} images/Picture5.png
:width: 50%
:align: center
```

Проверавамо да ли је ``a[srednji] == t``. У нашем случају видимо да је то сада тачно и прекидамо
претрагу јер смо нашли тражену вредност на индексу ``srednji = 1``.

```{questionnote}
Пробајте ово исто да урадите али да је тражена вредност ``t = 6``.
```

Бинарно претраживање је корисно када имате огроман број елемената. На пример, ако имате 1000
елемената. При првој подели број елемената где се тражи вредност пада на 500. При следећој
на 250 и тако редом.

```{infonote}
Бинарно претраживање може да се ради само код уређеног низа (било да је растући
ии опадајући)
```

Како би изгледао циклус који ради дељење низа на пола и проверу где се налази тражени елемент.

```c
donji = 0;
gornji = n - 1;
i = 0;
while (donji <= gornji && indeks < 0)
{
    srednji = (donji + gornji) / 2;
    if (a[srednji] == t)
        indeks = srednji;
    if (t < a[srednji])
        gornji = srednji - 1;
    else
        donji = srednji + 1;
}
```

```{questionnote}
Користећи *while* циклус изнад написати програм за бинарно претраживање уређеног низа.
```

**Решење**:

```c
#include <stdio.h> 
int main(void)
{
    int a[100], n, t, i, indeks = -1;
    int donji, gornji, srednji;
    printf("Koliko elemenata ima niz? ");
    scanf("%d", &n);
    printf("Unesi elemente u rastucem redosledu:\n");
    for (i = 0; i <= n - 1; i++)
    {
        printf("a[%d] = ", i);
        scanf("%d", &a[i]);
    }
    printf("Unesi element koji trazis: ");
    scanf("%d", &t);
    donji = 0;
    gornji = n - 1;
    i = 0;
    while (donji <= gornji && indeks < 0)
    {
        srednji = (donji + gornji) / 2;
        if (a[srednji] == t)
            indeks = srednji;
        if (t < a[srednji])
            gornji = srednji - 1;
        else
            donji = srednji + 1;
    }
    if (indeks >= 0)
        printf("\nTrazeni element postoji sa indeksom %d.", indeks);
    else
        printf("\nTrazeni element ne postoji.");
    return(0);
}

```
Можете приметити да и овде користимо промењиву ``indeks`` и додељујемо јој почетну
вредност -1. То значи да уколико он не промени вредност приликом подела тражени
елемент не постоји у низу.

**Излаз**:

```text
Koliko elemenata ima niz? 15
Unesi elemente u rastucem redosledu:
a[0] = 1
a[1] = 2
a[2] = 4
a[3] = 5
a[4] = 5
a[5] = 6
a[6] = 7
a[7] = 8
a[8] = 9
a[9] = 11
a[10] = 23
a[11] = 45
a[12] = 46
a[13] = 78
a[14] = 99
Unesi element koji trazis: 5

Trazeni element postoji sa indeksom 3.
```

```{questionnote}
Пробај овај задатак да допуниш тако што ћеш пре бинарног претраживања
проверити да ли је низ уређен. Уколико није, исписати поруку *Pre binarnog pretrazivanja niz mora da se uredi.*.
```
