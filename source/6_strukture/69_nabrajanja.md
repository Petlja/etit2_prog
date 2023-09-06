# Набрајања – enum

Набројиве константе су целобројне симболичке константе којима су вредности
додељене експлицитно или имплицитно набрајањем њихових имена у низу.

Општи облик набрајања би био:

```text
enum ime_nabrajanja { ime_konstante = vrednost, 
                 ....			
            ime konstante = vrednost};
```

`ime_nabrajanja` и `ime_konstante` су идентификатори.

Вредности су целобројни изрази, а уколико се изостави додела, сматра се да је
сваки наредни већи од претходног.

Такође, као и код структуре, може се дефинисати набројиви тип података.

Општи облик набројивог типа би био:

```text
typedef enum { ime_konstante=vrednost, 
			....
		ime_konstante=vrednost} Ime_типа;
```

`Ime_типа` је идентификатор. Изоставља се `ime_nabrajanja`.

Пример:

- набрајање:

```c
enum karte{
    KARO,
    PIK,
    HERC,
    TREF
};
```

```c
- набројиви тип:
typedef enum{
    KARO,
    PIK,
    HERC,
    TREF
} Karte;
```

Формално гледано, набројиви подаци су типа `int`. Првом пољу се аутоматски
додељује целобројна вредност 0 и за свако следеће се повећава за 1.

На пример…

```c
enum logicki {NE, DA};
```

…је набројиви тип назван `logicki` са две набројиве константе од којих прва
(`NE`) има вредност `0` а друга (`DA`) вредност `1`.

На пример:

```c
enum meseci {JAN = 1, FEB, MAR, APR, MAJ, JUN, JUL, AVG,SEP, OKT, NOV, DEC};
```

Набројива константа `JAN` има вредност 1, а свака следећа за 1 већу од
претходне.

На пример:

```c
typedef enum {CRNA, CRVENA, ZUTA, PLAVA, BELA} Boja;
Boja boja = CRVENA + 2;
```

У ствари, `boja` има вредност `PLAVA`.

Могуће је и експлицитно навођење целобројних вредности, на пример:

```c
enum znak_karte {
KARO = 1,
PIK = 2,
HERC = 4,
TREF = 8
}
```

Набројиви типови могу да учествују у изградњи других сложених типова.


Провери своје знање. Реши квиз.

<!---  PREFORMULISati PITANJA I ODGOVORE

Питање: У програмском језику С декларисан је структурни тип података `Ucenik`,
а затим и променљива `razred` која представља низ од максимум 30 ученика:

```c
typedef struct
{
    char ime[50];
    int razred;
    int ocene[10];
} Ucenik; 
…
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

Одговор: Тачан одговор је под 3. Други ученик има индекс 1 а четврта оцена
има индекс 3.

Питање: У програмском језику С декларисан је структурни тип података `Ucenik`,
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
…
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

Одговор: Тачан одговор је под 2. Први ученик има индекс 0, четврти предмет
има индекс 3 и поље оцена добија вредност 5.

Питање: У програмском језику C декларисани су структурни типови података
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

Одговор: Тачан одговор је под 2. Битан је редослед како су дефинисана поља у
структурама. Прво иде дестинација, па полазак и повратак у облику дан, месец,
година, и на крају цена.

Питање: У програмском језику C декларисани су структурни типови података `Tacka`
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

Одговор: Тачан одговор је под 4. Прво иде позиција тачке, а затим полупречник.

```{questionnote}
У програмском језику C декларисани су структурни типови података
`Zaposleni` и `Firma`, а затим и променљива типа `Firma`:
```

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
…
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

Одговор: Тачан одговор је под 1. У променљивој маркетинг радник на првој
позицији има индекс 0, а месец зараде има индекс 12, и то поље има вредност 10000.

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

Одговор: Тачан одговор је под 5. Помоћу `-> p` приступа пољу `osnova` а тачка
приступа пољу `brojTemena`.

У програмском језику С дефинисане су структуре које омогућавају груписање података
различитих типова. Дефинисати структурни тип податка `Ucenik` са пољима `ime`
(максимално 30 карактера), `prezime` (максимално 30 карактера) и `prosek` (типа
`double`). Одредити исправно написане декларације структурног типа `Ucenik`:

1. typedef struct ucenik{
char ime[30];
char prezime[30];
double prosek;
}Ucenik;

2. typedef struct ucenik{
char ime[31];
char prezime[31];
double prosek;
}Ucenik;

3. struct ucenik{
char ime[30];
char prezime[30];
double prosek;
}Ucenik;

4. typedef struct ucenik{
char ime[31],prezime[31];
double prosek;
}Ucenik;

Одговор: Тачан одговор је под 3 и 4. Не заборавите да на крају стринга једно
место заузима `'\n'`.

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

<!---  OVO NE MOŽE OVAKO DA PROĐE U ODGOVORIMA...

```{mchoice}
:answer1: djak.ocene[i]
:answer2: *djak.razred
:answer3: djak->ime
:answer4: djak[i].ocene
:answer5: djak.ime
:correct: 1,5

Одредити исправне начине приступа пољима структурне променљиве `djak`:
```



Одговор: Тачан одговор је под 1 и 5. Под 1 променљивој `djak` приступа се `i`-тој
оцени, а под 5 променљивој `djak` приступа се пољу `ime`.

Питање: У програмском језику C декларисан је структурни тип података `Putovanje`,
а затим и показивачка променљива `p`:

```text
 typedef struct
{
char start[50], cilj[50];
int predjeno_km;
}Putovanje; 
…
Putovanje *p;
```



```{mchoice}
:answer1: *p-> predjeno_km
:answer2: (*p). predjeno_km
:answer3: &p-> predjeno_km
:answer4: p->start
:answer5: *(p).start
:correct: 2,4

Одредити исправне начине приступа пољима структурне променљиве:
```



Одговор: Тачан одговор је под 2 и 4. Под 2 и под 4 *p је вредност.

Дата је декларација набројивог типа податка `boja`:

```c
enum boja {crna, plava=2, zelena, crvena=4, bela=15};
```

```{mchoice}
:answer1: crna = 0, plava = 2, zelena=3, crvena = 4, bela = 15
:answer2: crna = 1, plava = 2, zelena=3, crvena = 4, bela = 15
:answer3: crna = 0, plava = 1, zelena=3, crvena = 4, bela = 15
:correct: 1

Имајући у виду дефиницију набројивог типа податка, одредити вредности које
имају константе `crna`, `plava`, `zelena`, `crvena` и `bela`.
```

Одговор: Тачан одговор је под 1.

--->
