# Дефиниција структуре и структурног типа података

Структура је тип податка који дефинише програмер. Општи облик дефиниције
структуре би био:

```c
struct ime_strukture {
niz_deklaracija;
};
```

Име структуре је идентификатор који нема статус идентификатора типа, па се у
дефинисању променљиве из структуре увек испред пише `struct ime_strukture`.
Значи, само име структуре испред структурне променљиве није довољно.

Низом декларација набрајају се поља структуре. Свака декларација има облик:

```text
tip polje, polje ... polje;
```

Ово значи да, ако имамо више поља истог типа, можемо их навести под тим типом и
одвојити их зарезом. Наравно, можемо их навести и појединачно.

Битан је редослед навођења поља у оквиру структуре.
С обзиром да структура није тип податка при дефинисању идентификатора мора се испред навести struct ime_strukture
```text
struct ime_strukture str;
```
Приступ пољу структурне промењиве врши се навођењем структурног идентификатора затим `.` а након тога идентификатора поља. 
```text
str.polje;
```
```{image} images/image1.png
:width: 600
:align: center
```

```{questionnote}
Дефинишите структуру tacka која се састоји од два поља `x`, `y` типа
`int`. Напишите програм за унос и испис координата тачке `А`.
```

**Решење**:

```c
#include<stdio.h>
struct tacka
{
    int x,y;
};

int main(void)
{
    struct tacka A;
    printf("Unesi x koordinatu tacke A: ");
    scanf("%d", &A.x);
    printf("Unesi y koordinatu tacke A: ");
    scanf("%d", &A.y);
   printf("Uneli ste tacku A(%d, %d)", A.x, A.y);
   return 0;
}
```

Излаз:
```text
Unesi x koordinatu tacke A: 5
Unesi y koordinatu tacke A: 2
Uneli ste tacku A(5, 2)
```

Ако тачку А прикажемо у меморији:

```c
struct tacka A
```

```text
┌─────────┬─────────┐
| А.x = 5 | A.y = 2 |
└─────────┴─────────┘
```

С обзиром да име структуре није идентификатор типа, то можемо променити тако
што ћемо дефинисати структурни тип податка. У том случају, када се дефинише
структурна променљива није потребно да се испред пише struct. За дефинисање
новог типа користи се резервисана реч `typedef`.

Општи облик дефиниције структурног типа структуре би био:

```c
typedef struct ime_strukture {
    niz_deklaracija;
} ime_tipa;
```

Идентификатор `ime_tipa` може да се користи у дефинисању структурне променљиве
без службене речи `struct`.

Такође, при дефинисању структурног типа може се написати `ime_strukture`, али и
не мора.

Као што је претходно речено битан је редослед навођења поља у оквиру структуре.

```{questionnote}
Дефинишите структуру `tacka` увођењем новог типа `Tacka` која се састоји
од два поља `x`, `y` типа `int`. Написати програм за унос и испис координата
тачке `А`.
```

**Решење**:

```c
#include<stdio.h>
typedef struct {
    int x;
    int y;
} Tacka;

int main(void)
{
    Tacka A;
    printf("Unesi x koordinatu tacke A: ");
    scanf("%d", &A.x);
    printf("Unesi y koordinatu tacke A: ");
    scanf("%d", &A.y);
    printf("Uneli ste tacku A(%d, %d)", A.x, A.y);
}
```

Излаз:

```text
Unesi x koordinatu tacke A: 5
Unesi y koordinatu tacke A: 2
Uneli ste tacku A(5, 2)
```

Члановима структуре могу да се доделе почетне вредности, односно да се изврши
иницијализација.

Општи облик доделе почетних вредности структурној променљивој би био:

```text
struct ime_strukture promenjiva = {vrednost,vrednost...,vrednost};
```

```{questionnote}
Дефинишите структуру `tacka` која се састоји од два поља целобројног
типа података `x`, `y`. Тачки `О` доделити почетне вредности `x = 0`, `y = 0`, a
тачки `А` доделити почетне вредности `x = 1`, `y = 1`. Исти програм написати
користећи структурни тип `Tacka`. Исписати координате тачака `О` и `А`.
```
**Решење 1**:

```c
#include<stdio.h>
struct tacka {
    int x;
    int y;
};

int main(void)
{
    struct tacka O = {0, 0}, A = {1, 1};
    printf("Uneli ste tacku O(%d, %d) i tacku A(%d, %d)", O.x, O.y, A.x, A.y);
    return 0;
}
```

**Решење 2**:

```c
#include<stdio.h>
typedef struct {
    int x;
    int y;
} Tacka;

int main(void)
{
    Tacka O = {0, 0}, A = {1, 1};
    printf("Uneli ste tacku O(%d,%d) i tacku A(%d, %d)", O.x, O.y, A.x, A.y);
    return 0;
}
```

Излаз:

```text
Uneli ste tacku O(0, 0) i tacku A(1, 1)
```

Чланови структуре могу бити и друге структуре. Члан структуре не може бити
сама та структура, али њен члан може бити показивач на ту структуру.
Захваљујући тој чињеници касније ћемо дефинисати листе.

Анализирајмо следеће структуре:

1. `struct tacka { int x, y;};`
2. `struct tacka a,b,c,p = {35,-12}, q;`
3. `struct pravougaonik`
`{`
    `struct tacka dole_levo, gore_desno;`
`};`
4. `struct pravougaonik w, x, y = {{1, 1}, {3, 3}};`
5. `struct krug`
`{`
    `double r;`
    `struct tacka centar;`
`};`

Линијом 1 дефинисали смо структуру `tacka` са члановима `x`, `y` целобројног
типа.

Линијом 2 дефинисали смо променљиве `a`, `b`, `c`, `p`, `q` из структуре
`tacka` где променљива `p` има додељене вредности `x - 35`, `y - 12`.

Линијом 3 дефинисали смо структуру `pravougaonik` са члановима `dole_levo`,
`gore_desno` из структуре `tacka`.

Линијом 4 дефинисали смо променљиве `w`, `x`, `y` из структуре `pravougaonik`
где променљива `w` има додељене вредности тачака `dole_levo = {1, 1}`,
`gore_desno = {3, 3}`.

Линијом 5 дефинисали смо структуру `krug` са члановима `r` типа `double` и
`centar` из структуре `tacka`.

Ових пет линија кода можемо посматрати као део кода у коме се демонстрира примена структуре у структури.

```{questionnote}
Задатак: Дефинисати структурни тип `Ime` који садржи чланове `ime`, `prezime`
типа стринг (низ карактера) максималне дужине 20 карактера.

Дефинисати структурни тип `Datum` који садржи чланове `dan`, `mesec`, `godina`
типа `short int`.

Дефинисати структурни тип `Osoba` који садржи чланове типа `string JMBG`
максималне дужине 14 карактера, члан `osoba` структурног типа `Ime`, члан
`datum_rodjenja` структурног типа `Datum`, и `adresa` типа `string` максималне
дужине 30 карактера.

Креирати променљиве `lik1`, `lik2`, `lik3` из структурног типа `Osoba`.
```

**Решење**:

```C
typedef struct {char ime[20], prezime[20];} Ime;
typedef struct {short int dan, mesec, godina;} Datum;
typedef struct 
{
    char JMBG[14];
    Ime osoba;
    Datum datum_rodjenja;
    char adresa[30];
} Osoba;
Osoba lik1, lik2, lik3; 
```

Елементи структуре могу бити показивачи.

На пример структуру `Student` можемо декларисати на класичан начин…

```c
typedef struct {
    char ime[50];
    char prezime[50];
    double prosek;
} Student;
```

```{image} images/image2.png
:width: 600
:align: center
```

…или можемо користити показиваче:

```c
typedef struct {
    char *ime;
    char *prezime;
    double prosek;
} Student;
```

```{image} images/image3.png
:width: 600
:align: center
```
