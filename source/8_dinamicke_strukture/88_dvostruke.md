# Двоструко спрегнута листа

Рад са једноструко повезаним листама има извесне недостатке. Наиме, оне
омогућавају кретање кроз листу само у једном смеру. Даље, приликом брисања
елемента из листе потребно је чувати претходни елемент. Ако дође до губљења
везе у неком елементу, остали елементи постају недоступни, као карике ланца.

```{image} images/image24.jpg
:width: 500
:align: center
```

Ови проблеми се могу превазићи увођењем показивача и на претходни елемент. С
обзиром да показивач садржи адресу и свог следбеника и претходника, таква листа
се назива **двоструко спрегнута** или **двоструко повезана листа**.

```{image} images/image25.png
:width: 600
:align: center
:alt: Двоструко спрегнута листа
```

На почетку анализе ћемо дефинисати структуру, јер су елементи листе, као што
смо научили, структурног типа. Разлика у односу на једноструку листу јесте што
ова садржи још једно поље – показивач на претходни елемент.

```c
typedef struct lista
{
    int podatak;
    struct lista *prethodni, *sledeci;
} Lista;
```

## Додавање елемената у двоструко спрегнуту листу

Приликом додавања елемента у двоструко спрегнуту листу мора се водити рачуна о
исправном ажурирању показивача `prethodni` и `sledeci`, како би елементи били
успешно повезани. Параметри функције су показивач на први елемент `prvi`,
показивач показивач на последњи елемент `poslednji` и вредност која се уноси `n`.
Коришћење показивача на показивач омогућава одређене предности при ажурирању последњег 
елемента у листи. На пример, Његовим коришћењем не мора се пролазити кроз целу листу приликом додавања 
новог елемента, што побољшава ефикасност.
Ако је листа празна, ако је `prvi == NULL`, значи да додајемо први елемент у
листу.

Додељујемо меморију новом елементу – његов податак добија вредност унетог
елемента `n`. Постављамо његове показиваче `prethodni` и `sledeci` на `NULL`.
Показивач на последњи елемент `poslednji` ажурирамо тако да показује на нови
елемент.

Ако листа није празна, желимо да додамо елемент на крај листе. После доделе меморије и
вредности `n` новом елементу, ажурирамо његов показивач `prethodni` да показује
на тренутно последњи елемент, онај на који указује показивач `poslednji`.
Показивач `sledeci` се поставља на `NULL`.

Затим се ажурира показивач `sledeci` тренутно последњег елемента на нови
елемент. Показивач `poslednji` се поставља да показује на нови елемент, који је
сада последњи елемент.

Функција на крају враћа показивач на први елемент листе `prvi`.

Функција за додавање елемента у двоструко повезану листу би изгледала овако:

```c
Lista* dodaj(Lista* prvi, Lista** poslednji, int n)
{
    Lista* pom; 
    if (prvi == NULL)
    {
        prvi = (Lista*)malloc(sizeof(Lista));
        if (prvi == NULL)
        {
            printf("Greska!\n");
            exit(0);
        }
        prvi->podatak = n;
        prvi->prethodni = prvi->sledeci = NULL;
        *poslednji = prvi;
    }
    else
    {
        pom = (Lista*)malloc(sizeof(Lista));
        if (pom == NULL)
        {
            printf("Greska.\n");
            exit(0);
        }
        pom->podatak = n;
        pom->prethodni = (*poslednji);
        pom->sledeci = NULL;
        (*poslednji)->sledeci = pom;
        (*poslednji) = pom;
    }
    return (prvi);
}
```

## Испис елемената двоструко спрегнуте листе унапред

Функција за штампање унапред:
    Код ове функције показивач p који се прослеђује као аргумент показује на први елемент 
    двоструко спрегнуте листе.

```c
void stampaj_unapred(Lista* p)
{
    printf("Elementi liste stampani unapred su:\n");
    while (p != NULL)
    {
        printf("%d\t", p->podatak);
        p = p->sledeci;
    }
    printf("\n");
}
```

```{image} images/image26.png
:width: 600
:align: center
:alt: Пролаз кроз листу и штампање унапред, од првог до последњег елемента
```

## Испис елемената двоструке спрегнуте листе уназад

Функција за штампање уназад:
    Код ове функције показивач p који се прослеђује као аргумент показује на последњи елемент 
двоструко спрегнуте листе.

```c
void stampaj_unazad(Lista* p)
{
    printf("Elementi liste stampani unazad su:\n");
    while (p != NULL)
    {
        printf("%d\t", p->podatak);
        p = p->prethodni;
    }
    printf("\n");
}
```

```{image} images/image27.png
:width: 600
:align: center
:alt: Пролаз кроз листу и штампање уназад, од последњег до првог елемента
```

## Број елемената у двоструко спрегнутој листи

Функција одређивања броја елемената у листи:
    Овај алгоритам се реализује исто као у случају једноструко спрегнуте листе, јер су нам једино потребни 
показивачи унапред.


```c
int duzina(Lista* p)
{
    int broj = 0;
    while (p != NULL)
    {
        broj++;
        p = p->sledeci;
    }
    return(broj);
}
```

## Брисање елемената из двоструко спрегнуте листе

Приликом брисања елемената из двоструко спрегнуте листе није неопходно знати показивач на
претходни елемент листе. Та информација је била неопходна код једноструких
листа. Ово је могуће зато што сваки елемент двоструке листе садржи показивач и
на претходни и на наредни елемент.

Неопходно је знати редни број у листи који желимо да бришемо. Наравно, треба
водити рачуна о унетој позицији.

Показивач `pom` се поставља на почетак листе и иницијализује вредност на 1.
Кретањем кроз листу проналазимо и бришемо елемент на задатој позицији.

Ако елемент који се брише има претходника, његов показивач се ажурира тако да
прескаче елемент који се брише. Он сада показује на следећи елемент брисаног
елемента.

Ажурира се и показивач `sledeci` претходника елемента који се брише. Такође се
ажурира показивач `prethodni` наредног елемента од елемента који се брише. На
овај начин се прескаче брисани елемент.

На крају се ослобађа меморија коју заузима елемент који се брише.

Функција враћа показивач на први елемент листе.

Функција за брисање елемента из двоструко повезане листе:

```c
Lista* obrisi(Lista* prvi, Lista** poslednji, int redni_broj)
{
    Lista* pom;
    int i;
    if (redni_broj <= 0 || redni_broj > duzina(prvi))
    {
        printf("Greska! Element ne postoji u listi.\n");
        exit(0);
    }
    pom = prvi;
    i = 1;
    while (i < redni_broj)
    {
        i = i + 1;
        pom = pom->sledeci;
    }
    if (pom->prethodni != NULL)
        pom->prethodni->sledeci = pom->sledeci;
    else
        prvi = pom->sledeci;
    if (pom->sledeci != NULL)
        pom->sledeci->prethodni = pom->prethodni;
    else
        (*poslednji) = pom->prethodni;
    free(pom);
    return (prvi);
}
```

```{image} images/image28.png
:width: 600
:align: center
:alt: Брисање елемента из двоструке листе
```

```{questionnote}
Користећи претходно креиране функције написати програм за
симулацију основних операција у раду са двоструко спрегнутом листом.
```

```c
Lista* dodaj(Lista* prvi, Lista** poslednji, int n);
void stampaj_unapred(Lista* p);
void stampaj_unazad(Lista* p);
int duzina(Lista* p);
Lista* obrisi(Lista* prvi, Lista** poslednji, int redni_broj);

int main(void)
{
    int n, i;
    int vrednost;
    Lista* pocetak = NULL;
    Lista* kraj = NULL;
    printf("Unesite broj elementa liste:\n");
    scanf("%d", &n);
    for (i = 0; i < n; i++)
    {
        printf("Unesi vrednost:\n");
        scanf("%d", &vrednost);
        pocetak = dodaj(pocetak, &kraj, vrednost);
    }
    printf("Kreirana lista je:\n");
    stampaj_unapred(pocetak);
    stampaj_unazad(kraj);
    printf("Unesite redni broj elementa koji treba obrisati:\n");
    scanf("%d", &n);
    pocetak = obrisi(pocetak, &kraj, n);
    printf("Lista posle brisanja %d. elementa je:\n", n);
    stampaj_unapred(pocetak);
    stampaj_unazad(kraj);
    return 0;
}
```

Резултат главног програма:

```text
Unesite broj elementa liste:
5
Unesi vrednost:
1
Unesi vrednost:
2
Unesi vrednost:
3
Unesi vrednost:
4
Unesi vrednost:
5
Kreirana lista je:
Elementi liste  stampani unapred su:
1       2       3       4       5
Elementi liste  stampani unazad su:
5       4       3       2       1
Unesite redni broj elementa koji treba obrisati:
3
Lista posle brisanja 3. elementa je:
Elementi liste  stampani unapred su:
1       2       4       5
Elementi liste  stampani unazad su:
5       4       2       1
```
