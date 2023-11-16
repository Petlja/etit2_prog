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



