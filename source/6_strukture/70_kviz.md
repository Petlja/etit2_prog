# Шта смо научили
## Реши квиз
```{questionnote}
У програмском језику С декларисан је структурни тип података `Ucenik`,
а затим и променљива `razred` која представља низ од максимум 30 ученика:

```c
typedef struct
{
    char ime[50];
    int razred;
    int ocene[10];
} Ucenik; 

Ucenik razred[30];
```
```{mchoice}
:answer1: razred[0].ocene[3]=’5’; 
:answer2: razred [1].ocene[4]=5;
:answer3: razred[1].ocene[3]=5;
:answer4: razred.ocene[3]=5;
:correct: 3

Одреди наредбу којом се другом ученику у низу `razred` уписује оцена 5 из
математике, ако знамо да је математика четврта оцена у низу оцена:
```
```{questionnote}
У програмском језику С декларисан је структурни тип података `Ucenik`,
а затим и променљива `razred` која представља низ од максимум 30 ученика:

```c
typedef struct
{
    char naziv[30];
    int razred, ocena;
} Predmet;

typedef struct
{
    char ime[20], prezime[20];
    Predmet predmeti[10];
} Ucenik;

Ucenik razred[30];
```

```{mchoice}
:answer1: razred.[0]->predmeti[3]->ocena=5;
:answer2: razred [0].predmeti[3].ocena=5;
:answer3: razred [0].predmeti[“matematika”].ocena=5;
:answer4: razred.ocena[3]=5;
:correct: 2

Одреди наредбу којом се првом ученику у низу `razred` уписује оцена 5 из
математике, ако знамо да је математика четврта оцена у низу оцена:
```
```{questionnote}
У програмском језику C декларисани су структурни типови података
`Datum` и `Letovanje`:

```c
typedef struct
{
    int dan, mesec, godina;
} Datum;

typedef struct
{
    char destinacija[50];
    Datum polazak, povratak;
    float cena;
} Letovanje;
```


```{mchoice}
:answer1: Letovanje odmor = {" Atina ",{2023,8,10},{2023,8,21},500};
:answer2: Letovanje odmor = {" Atina ",{10,8,2023},{21,8,2023},500};
:answer3: Letovanje odmor = {" Atina ",{10,8,2023,21,8,2023},500};
:answer4: Letovanje odmor = { Atina,{2023,8,10},{2023,8,21},500};
:answer5: Letovanje odmor = {" Atina ",500,{2023,8,10},{2023,8,21}};
:correct: 2

Одреди исправно написану наредбу декларације и иницијализације променљиве `odmor`
типа `Letovanje`, ако је дестинација `Atina`, полазак `10.08.2023.`, а повратак
`21.08.2023.` Цена је `500€`.
```
```{questionnote}
У програмском језику C декларисани су структурни типови података `Tacka`
(који дефинише тачку у простору) и `Lopta` (одређена центром и полупречником):

```c
typedef struct
{
    float x, y, z;
} Tacka;

typedef struct
{
    Tacka centar;
    float R;
} Lopta;
```

```{mchoice}
:answer1: Lopta L = {50, {0, 0, 0}};
:answer2: Lopta L = {0, 0, 0, 50};
:answer3: Lopta L = {0, 0, 0}, {50};
:answer4: Lopta L = {{0, 0, 0}, 50};
:correct: 4

Одредити исправно написану наредбу декларације и иницијализације променљиве `L`
типа `Lopta`, тако да јој центар буде у тачки `О(0,0,0)`, а полупречник `50 cm`:
```

```{questionnote}
У програмском језику C декларисани су структурни типови података
`Zaposleni` и `Firma`, а затим и променљива типа `Firma`:

```c
typedef struct
{
    char ime[50], prezime[50];
    float zarada[12];
} Zaposleni;

typedef struct
{
    char naziv[50];
    Zaposleni radnici[200];
} Firma;

Firma marketing;
```

```{mchoice}
:answer1: marketing.radnici[0].zarade[11]=100000;
:answer2: marketing[0].radnici[0].zarade[11]=100000;
:answer3: marketing.radnici[1].zarade[12]=100000;
:answer4: marketing[0].radnici.zarade[11]=100000;
:correct: 1

Одредити наредбу којом се раднику, који се у евиденцији одељења `marketing`
налази на првој позицији, уписује плата за децембар у износу од 100.000 дин:
```

```{questionnote}
У програмском језику C декларисани су структурни типови података `Tacka`
(одређена координатама), `Poligon` (одређен бројем и координатама темена) и `Piramida`
(одређена типом основе – троугао, четвороугао... и висином). Потом је декларисана и
показивачка променљива  p:
```

```c
typedef struct
{
    float x, y;
} Tacka;

typedef struct
{
    int brojTemena;
    Tacka temena[10];
} Poligon;

typedef struct
{
    Poligon osnova;
    float visina;
} Piramida;
...
Piramida *p;
```
```{mchoice}
:answer1: p.osnova.brojTemena=6;
:answer2: p.osnova->brojTemena=6;
:answer3: p->osnova->brojTemena=6;
:answer4: p->osnova[brojTemena]=6;
:answer5: p->osnova.brojTemena=6;
:correct: 5

Одредити наредбу којом се број темена основе пирамиде на коју показује
декларисани показивач `*p`, поставља на 6:
```
```{questionnote}
У програмском језику С дефинисане су структуре које омогућавају груписање података
различитих типова. Дефинисати структурни тип податка `Ucenik` са пољима `ime`
(максимално 30 карактера), `prezime` (максимално 30 карактера) и `prosek` (типа
`double`). 
```
```{mchoice}
:answer1: typedef struct ucenik{char ime[30]; char prezime[30]; double prosek;}Ucenik;
:answer2: typedef struct ucenik{char ime[31]; char prezime[31]; double prosek;}Ucenik;
:answer3: struct ucenik{char ime[30]; char prezime[30]; double prosek;}Ucenik;
:answer4: typedef struct ucenik{char ime[31], prezime[31]; double prosek;}Ucenik;
:correct: 2,4
Одредити исправно написане декларације структурног типа `Ucenik`:
```
<!---  OVO NE MOŽE OVAKO DA PROĐE U ODGOVORIMA...
Питање: У програмском језику C декларисан је структурни тип података `Ucenik`,
а затим и променљива типа `Ucenik`:

```text
typedef struct
{
char ime[50];
int razred;
int ocene[10];
}Ucenik; 
…
int i; Ucenik djak;
```

```{mchoice}
:answer1: djak.ocene[i]
:answer2: *djak.razred
:answer3: djak->ime
:answer4: djak[i].ocene
:answer5: djak.ime
:correct: 1,5

Одредити исправне начине приступа пољима структурне променљиве `djak`:
```
--->
