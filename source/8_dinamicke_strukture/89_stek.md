# Стек

Стек је LIFO (*Last In-First Out*) техника смештања података. Чвор који је
последњи постављен у стек се први узима са врха стека.

```{image} images/image29.jpg
:width: 250
:align: center
:alt: Илустрација стека
```

Стек има велику примену у програмирању. Локалне променљиве у функцији се чувају
на стеку, а када функција заврши са радом, склањају се са стека. Користи се
такође приликом позива функција и повратка из њих. Многи међурезултати
израчунавања и рекурзивни проблеми користе стек. Ово су само неки од примера
примене стека.

И примера из живота има пуно. Јеси ли се запитао како се у веб-претраживачу
кликом на дугме назад или напред враћаш на странице које си већ посетио? Где се
и како чувају њихове адресе?

Такође, када користиш програме за обраду текста, слика или табела, сигурно си
користио захвалне наредбе Undo и Redo.

Стек структура омогућава да се акције које си користио памте тако да се могу
поништити и касније вратити.

Стек има две основне операције:

- додавање елемента на врх стека (енгл. *push*), и
- скидање елемента са врха стека (енгл. *pop*).

Можемо направити паралелу стека са низовима. Врху стека би одговарао последњи
елемент низа. Операција додавања на стек одговара додавању елемента на крај
низа. Наравно, скидање елемента са врха стека одговара узимању последњег
елемента низа.

Стекове најчешће имплементирамо преко листи. Функцији `dodaj_na_stek` би
одговарала функција `dodaj_na_pocetak_liste`.

Функцији `skini_sa_steka` би одговарала функција `obrisi_sa_pocetka_liste`.

Функција `skini_sa_steka`, осим што брише елемент са врха, треба да врати нову
вредност која се налази на врху после скидања старе. С обзиром да са празног
стека не можемо ништа скинути, ова функција треба да врати информацију да ли је
скидање успело.

На почетку анализе поново ћемо дефинисати структуру, јер су елементи листе, као
што смо научили, структурног типа.

```c
typedef struct lista 
{
    int podatak;
    struct lista *sl_adresa;
} Lista;
```

## Додавање елемената на стек

Као што смо навели на почетку приче о стеку, нови елемент или чвор додајемо на
врх стека. Овај поступак се назива `push`, па ћеш често у литератури наћи да се
тако именује и функција. У нашој функцији са `vrh` смо означили показивач на
први елемент, односно врх стека.

Ако си савладао додавање елемента на почетак листе, биће ти лако да схватиш ову
функцију. Обрати пажњу да смо користили функцију `exit` која прекида извршење
програма ако је дошло до грешке.

```c
Lista* dodaj_na_stek(Lista* vrh, int vrednost)
{
    Lista* novi;
    novi = (Lista*)malloc(sizeof(Lista));
    if (novi == NULL)
    {
        printf("Greska!");
        exit(0);
    }
    novi->podatak = vrednost;
    novi->sl_adresa = vrh;
    vrh = novi;
    return (vrh);
}
```

```{image} images/image30.png
:width: 600
:align: center
:alt: Додавање елемента на врх стека
```

## Скидање елемента са стека

Скидање елемента са стека врши се брисањем последњег додатог елемента у стек.
То је заправо брисање првог елемента у листи. Овај поступак се често назива
`pop`.

```c
Lista* skini_sa_steka(Lista* vrh, int* podatak)
{
    Lista* novi;
    if (vrh == NULL)
    {
        printf("Greska");
        exit(0);
    }
    *podatak = vrh->podatak;
    novi = vrh;
    vrh = vrh->sl_adresa;
    free(novi);
    return vrh;
}
```

```{image} images/image31.png
:width: 600
:align: center
:alt: Брисање елемента са врха стека
```

## Испис елемената стека

Испис елемената стека се врши проласком кроз листу, коришћењем показивача
`tekuci`, који на почетку добија адресу врха стека. Након обраде првог елемента
листе, `tekuci` добија вредност показивача на следећи елемент, обрађује податак
и тако све до краја листе док не добије вредност `NULL`, што би одговарало
последњем елементу листе.

```c
void ispis_steka(Lista* vrh) 
{
    Lista* tekuci;
    tekuci = vrh;
    printf("Elementi steka su:\n");
    while (tekuci != NULL) 
    {
        printf("%d ", tekuci->podatak);
        tekuci = tekuci->sl_adresa;
    }
    printf("\n");
}
```

```{image} images/image32.png
:width: 600
:align: center
:alt: Пролазак кроз стек и испис елемената стека
```

## Брисање стека

Приликом брисања се унутар петље креира привремени показивач `temp` и поставља
на тренутни чвор на који показује `tekuci`. Показивач се ажурира да показује на
следећи чвор, а меморија коју алоцира `temp` се брише. На тај начин се чвор
уклања из стека. Петља се наставља све док се не дође до краја, односно док сви
чворови у стеку не буду ослобођени.

На крају петље, стек ће бити обрисан.

```c
void obrisi_stek(Lista* vrh)
{
    Lista* tekuci;
    tekuci = vrh;
    while (tekuci != NULL) 
    {
        Lista* temp = tekuci;
        tekuci = tekuci->sl_adresa;
        free(temp);
    }
}
```

## Дужина стека

Дужина или број елемената стека добија се проласком кроз петљу. Вредност
локалне променљиве `broj` инкрементира се увек када показивач `tekuci` покаже
на чвор стека.

```c
int duzina_steka(Lista* vrh)
{
    Lista* tekuci;
    tekuci = vrh;
    int broj = 0;
    while (tekuci != NULL)
    {
        broj++;
        tekuci = tekuci->sl_adresa;
    }
    return (broj);
}
```

```{questionnote}
Користећи претходно креиране функције, написати програм за симулацију основних операција у раду са стеком.
```

```c
Lista* dodaj_na_stek(Lista* p, int vrednost);
Lista* skini_sa_steka(Lista* vrh, int* podatak);
void ispis_steka(Lista* vrh);
int duzina_steka(Lista* vrh);
void obrisi_stek(Lista* vrh);

int main(void)
{
    Lista* vrh = NULL;
    int n, i, vrednost;
    printf("Unesi broj elemenata steka:\n");
    scanf("%d", &n);
    for (i = 0;i < n;i++)
    {
        printf("Unesite %d. element u stek: ", i + 1);
        scanf("%d", &vrednost);
        vrh = dodaj_na_stek(vrh, vrednost);
    }
    ispis_steka(vrh);
    vrh = skini_sa_steka(vrh, &vrednost);
    ispis_steka(vrh);
    printf("Duzina steka je %d\n", duzina_steka(vrh));
    obrisi_stek(vrh);
    vrh = NULL;
    if (duzina_steka(vrh) == 0)
        printf("Stek je prazan");
}
```

Резултат извршавања програма:

```text
Unesi broj elemenata steka:
5
Unesite 1. element u stek: 1
Unesite 2. element u stek: 2
Unesite 3. element u stek: 3
Unesite 4. element u stek: 4
Unesite 5. element u stek: 5
Elementi steka su:
5 4 3 2 1
Elementi steka su:
4 3 2 1
Duzina steka je 4
Stek je prazan
```

Елементи стека не морају бити само бројеви. У наредном задатку ћемо симулирати
рад веб-прегледача. Наравно, имена посећених сајтова који представљају улазне
податке у нашем стеку су стрингови.

```{suggestionnote}
Ово је само основна верзија. На
[Петљи](https://petlja.org/biblioteka/r/Zbirka2/istorija_pregledaca)
покушај да решиш задатак који представља мало сложенију анализу прегледача.
```

```c
#include<stdio.h>
#include<stdlib.h>
#include<string.h>
 
typedef struct lista 
{
    char podatak[30];
    struct lista* sl_adresa;
} Lista;
 
Lista* dodaj_na_stek(Lista* p, char red[])
{
    Lista* novi;
    novi = (Lista*)malloc(sizeof(Lista));
    if (novi == NULL)
    {
        printf("Greska!");
        exit(0);
    }
    strcpy(novi->podatak, red);
    novi->sl_adresa = p;
    p = novi;
    return (p);
}
 
void ispis_steka(Lista* p) 
{
    while (p != NULL) 
    {
        puts(p->podatak);
        p = p->sl_adresa;
    }
    printf("\n");
}
 
Lista* skini_sa_steka(Lista* p, char red[]) 
{
    Lista* novi;
    if (p == NULL) 
    {
        printf("Greska");
        exit(0);
    }
    strcpy(red, p->podatak);
    novi = p;
    p = p->sl_adresa;
    free(novi);
    return p;
}

void obrisi_stek(Lista* vrh)
{
    Lista* tekuci;
    tekuci = vrh;
    while (tekuci != NULL) 
    {
        Lista* temp = tekuci;
        tekuci = tekuci->sl_adresa;
        free(temp);
    }
}
 
int main(void)
{
    Lista* vrh = NULL;
    int n, i, vrednost;
    char red[30];
    printf("Unesi broj sajtova koje posecujes:\n");
    scanf("%d", &n);
    getchar();
    for (i = 0;i < n;i++)
    {
        gets(red);
        vrh = dodaj_na_stek(vrh, red);
    }
    printf("Posetio si sajtove:\n");
    ispis_steka(vrh);
    return 0;
}
```

```text
Unesi broj sajtova koje posecujes:
5
http://www.rts.rs
http://www.petlja.org
http://politikin-zabavnik.co.rs
www.b92.net/sport
https://prosveta.gov.rs

Posetio si sajtove:
https://prosveta.gov.rs
www.b92.net/sport
http://politikin-zabavnik.co.rs
http://www.petlja.org
http://www.rts.rs
```
