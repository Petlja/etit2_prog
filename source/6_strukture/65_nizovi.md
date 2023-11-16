# Низови структура

Видели смо да низ може бити члан структуре. С обзиром да је низ скуп елемената
истог типа, може се направити низ који чине елементи исте структуре.

Задатак: Дефинисати структурни тип `Osoba` који садржи чланове типа
`string imeprezime` максималне дужине 40 карактера и `pol` максималне дужине 7
карактера, `god_starosti` типа `int`. Креирати низ структура `spisak` типа `Особа`
од максимално 10 елемената.

Решење:

```c
#include<stdio.h>
typedef struct
{
    char imeprezime[40];
    char pol[7];
    int godine;
} Osoba;

int main(void)
{
    Osoba spisak[10];
    int i, n;
    printf("Unesi broj osoba < 11: ");
    scanf("%d", &n);
    getchar();
    for(i = 0; i < n; i++)
    {
        printf("Unesi ime i prezime osobe %d: ", i + 1);
        gets(spisak[i].imeprezime);	
        printf("Unesi pol osobe %d: ",i + 1);
        gets(spisak[i].pol);
        printf("Unesi godine osobe %d: ", i + 1);
        scanf("%d", &spisak[i].godine);
        getchar();	
    }
    printf("\nUneli ste spisak\n");
    for(i = 0; i < n; i++)
        printf("%d. %s %s %d godina\n", i + 1, spisak[i].imeprezime, spisak[i].pol, spisak[i].godine);
    return 0;
}
```

Излаз:

```text
Unesi broj osoba < 11: 4
Unesi ime i prezime osobe 1: Pero Peric
Unesi pol osobe 1: muski
Unesi godine osobe 1: 25
Unesi ime i prezime osobe 2: Milica Petric
Unesi pol osobe 2: zenski
Unesi godine osobe 2: 17
Unesi ime i prezime osobe 3: Marko Markovic
Unesi pol osobe 3: muski
Unesi godine osobe 3: 32
Unesi ime i prezime osobe 4: Marija Marjanovic
Unesi pol osobe 4: zenski
Unesi godine osobe 4: 28

Uneli ste spisak
1. Pero Peric muski 25 godina
2. Milica Petric zenski 17 godina
3. Marko Markovic muski 32 godina
4. Marija Marjanovic zenski 28 godina
```

Низу елемената структурног типа такође се могу доделити почетне вредности
(иницијализација).

```{questionnote}
Дефинисати структурни тип `Godina` који садржи члан месец типа
`string` максималне дужине 10 карактера и `br_dana` типа `int`. Извршити
иницијализацију структурног низа `kalendar` користећи структурни тип `Godina`.
Након тога исписати садржај низа `kalendar`.
```

**Решење**:

```c
#include<stdio.h>
typedef struct
{
    char mesec[10];
    int br_dana;
} Godina;

int main(void)
{
    int i;
    Godina kalendar[] = {{"januar", 31}, {"februar", 28},
        {"mart", 31}, {"april", 30},{"maj", 31}, {"jun", 30}, 
        {"jul", 31}, {"avgust", 31}, {"septembar", 30}, 
        {"oktobar", 31}, {"novembar", 30}, {"decembar", 31}
    };
    printf("U nizu kalendar su elementi \n");
    for(i = 0; i < 12; i++)
        printf( "%s \t %d\n", kalendar[i].mesec, kalendar[i].br_dana);
    return 0;
}
```

Излаз:

```text
U nizu kalendar su elementi
januar 31
februar 28
mart 31
april 30
maj 31
jun 30
jul 31
avgust 31
septembar 30
oktobar 31
novembar 30
decembar 31
```
