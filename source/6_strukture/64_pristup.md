# Приступ члановима структуре

Пољима структуре приступа се помоћу оператора тачка (`.`).

Први операнд преставља операнд структуралног типа, а други је идентификатор
поља коме се приступа.

Нпр. у структури `s` пољу `p` се приступа са `s.p`

```{image} images/image4.png
:width: 110
:align: center
```

Ако је `ps` показивач на структуру а `p` поље структуре, приступа се помоћу `(*ps).p`

```{image} images/image5.png
:width: 200
:align: center
```

Заграде су обавезне јер, у недостатку заграда, због вишег приоритета оператора
тачка у односу на `*` израз би се тумачила као `*(ps.p)`, што значи да не
показује на структуру већ на поље у структури.

Због честе употребе показивача дефинисан је бинарни оператор `->` за приступ
пољу `p` структуре на коју указује показивач `ps`. Пише се `ps->p`.

Оба бинарна оператора, тачка и `->`, истог су приоритета и групишу се са лева
на десно.

Задатак: Дефинисати структурни тип `Licnost` који садржи чланове типа
`string ime_prezime` максималне дужине 30 карактера и `adresa` максималне
дужине 40 карактера, као и члан `godine` типа `int`. Написати програм којим се
уносе подаци о две особе, а затим одређује која је особа старија. Задатак
решити преко вредносних променљивих а затим преко показивача.

**Решење 1**:

```c
#include<stdio.h>
typedef struct
{
    char imeiprezime[30];
    char adresa[40];
    int godine;
} Licnost;

int main(void)
{
    Licnost osoba1, osoba2, stariji;
    printf("Unesi ime prve osobe: ");
    gets(osoba1.imeiprezime);
    printf("Unesi adresu prve osobe: ");
    gets(osoba1.adresa);
    printf("Unesi starost prve osobe: ");
    scanf("%d",&osoba1.godine);
    getchar();// mora da pokupi enter odnosno '\n' pre gets
    printf("Unesi ime druge osobe: ");
    gets(osoba2.imeiprezime);
    printf("Unesi adresu druge osobe: ");
    gets(osoba2.adresa);
    printf("Unesi starost druge osobe: ");
    scanf("%d", &osoba2.godine);
    if(osoba1.godine == osoba2.godine)
        printf("Osobe su istih godina\n");
    else
        {
            if (osoba1.godine<osoba2.godine)
                stariji = osoba2;
            else
                stariji = osoba1;
            printf("Starija osoba je:\n");
            printf("%s %s star: %d", stariji.imeiprezime, stariji.adresa, stariji.godine);
        }
    return 0;
}
```

**Решење 2**:

```c
#include<stdio.h>
typedef struct
{
    char imeiprezime[30];
    char adresa[40];
    int godine;
} Licnost;

int main(void)
{
    Licnost osoba1, osoba2, stariji, *p1,*p2,*s;
    p1 = &osoba1;
    p2 = &osoba2;
    s = &stariji;
    printf("Unesi ime prve osobe: ");
    gets(p1->imeiprezime);
    printf("Unesi adresu prve osobe: ");
    gets(p1->adresa);
    printf("Unesi starost prve osobe: ");
    scanf("%d",p1->godine);
    getchar();// mora da pokupi enter odnosno '\n' pre gets 
    printf("Unesi ime druge osobe: ");
    gets(p2->imeiprezime);
    printf("Unesi adresu druge osobe: ");
    gets(p2->adresa);
    printf("Unesi starost druge osobe: ");
    scanf("%d", p2->godine);
    if (p1->godine == p2->godine)
        printf("Osobe su istih godina\n");
    else
        {
            if (p1->godine < p2->godine)
                s = p2;
            if (p2->godine < p1->godine)
                s = p1;
            printf("Starija osoba je:\n");
            printf("%s %s star:%d", s->imeiprezime, s->adresa, s->godine);
	    }
    return 0;
}
```

Излаз:

```text
Unesi ime prve osobe: Pero Peric
Unesi adresu prve osobe: Mikina 25 Kraljevo
Unesi starost prve osobe: 25
Unesi ime druge osobe: Marko Markovic
Unesi adresu druge osobe: Milana Toplice 11 Nis
Unesi starost druge osobe: 36
Starija osoba je:
Marko Marovic Miana Toplice 11 Nis star: 36
```

Излаз:

```text
Unesi ime prve osobe: Pero Peric
Unesi adresu prve osobe: Mikina 25 Kraljevo
Unesi starost prve osobe: 25
Unesi ime druge osobe: Marko Markovic
Unesi adresu druge osobe: Milana Toplice 11 Nis
Unesi starost druge osobe: 25
Osobe su istih godina
```

```{questionnote}
Дефинисати структурни тип `Datum` са пољима `dan`, `mesec`, `godina`
типа `int`. Дефинисати структурни тип `Student` који садржи поља типа стринг
`prezime` и `ime` максималних дужина 20 карактера, поље `dat_rodj` структурног
типа `Datum`, поље `god_studija` типа `int` и поља `prosecna_ocena` типа
`float`.

1. Иницијализовати податке за једног студента и исписати његове податке.
2. Са стандардног улаза унети, а затим исписати податке за једног студента.
```

**Решење 1**:

```c
#include<stdio.h>
typedef struct
{
    int dan;
    int mesec;
    int godina;
} Datum;

typedef struct
{
    char prezime[20];
    char ime[20];
    Datum dat_rodj;
    int god_studija;
    float prosecna_ocena;
} Student;

int main(void)
{
    Student std = {"Marko","Markovic", 14, 5, 1995, 3, 6.58};
    //Student std = {"Marko","Markovic",{14, 5, 1995}, 3, 6.58};
    printf("Uneli ste studenta\n");
    printf("Ime i prezime: %s %s\n", std.ime, std.prezime);
    printf("Datum rodjenja: %d.%d.%d\n",std.dat_rodj.dan, std.dat_rodj.mesec, std.dat_rodj.godina);
    printf("Godina studija: %d\n", std.god_studija);
    printf("Prosecna ocena: %.2f\n", std.prosecna_ocena);
    return 0;
}
```

Излаз:

```text
Uneli ste studenta
Ime i prezime: Marko Markovic
Datum rodjenja: 14.5.1995
Godina studija: 3
Prosecna ocena: 6.58
```

**Решење 2**:

```c
#include<stdio.h>
typedef struct
{
    int dan;
    int mesec;
    int godina;
} Datum;

typedef struct
{
    char prezime[20];
    char ime[20];
    Datum dat_rodj;
    int god_studija;
    float prosecna_ocena;
} Student;

int main(void)
{
    Student std;
    printf("Unesi ime studenta: ");
    gets(std.ime);
    printf("Unesi prezime studenta: ");
    gets(std.prezime);
    printf("Unesi datum rodjenja: ");
    scanf("%d", &std.dat_rodj.dan);
    printf("Unesi mesec rodjenja: ");
    scanf("%d", &std.dat_rodj.mesec);
    printf("Unesi godinu rodjenja: ");
    scanf("%d", &std.dat_rodj.godina);
    printf("Unesi godinu studija: ");
    scanf("%d", &std.god_studija);
    printf("Unesi prosecnu ocenu: ");
    scanf("%f", &std.prosecna_ocena);
    printf("\nUneli ste studenta\n");
    printf("Ime i prezime: %s %s\n",std.ime, std.prezime);
    printf("Datum rodjenja: %d.%d.%d\n", std.dat_rodj.dan, std.dat_rodj.mesec, std.dat_rodj.godina);
    printf("Godina studija: %d\n", std.god_studija);
    printf("Prosecna ocena: %.2f\n", std.prosecna_ocena);
    return 0;
}
```

Излаз:

```text
Unesi ime studenta: Marko
Unesi prezime studenta: Markovic
Unesi datum rodjenja: 14
Unesi mesec rodjenja: 5
Unesi godinu rodjenja: 1995
Unesi godinu studija: 3
Unesi prosecnu ocenu: 6.58

Uneli ste studenta
Ime i prezime: Marko Markovic
Datum rodjenja: 14.5.1995
Godina studija: 3
Prosecna ocena: 6.58
```

```{questionnote}
Дефинисати структурни тип `Datum` са пољима `dan`, `mesec`, `godina`
типа `int`. Дефинисати структурни тип `Student` који садржи поља типа стринг
`prezime` и `ime` максималних дужина 20 карактера, поље `dat_rodj` структурног
типа `Datum`, поље `god_studija` типа `int` и поља `prosecna_ocena` типа
`float`. Са стандардног улаза унети а затим исписати податке за једног
студента. Приступ пољима структуре одрадити преко показивача.
```

**Решење**:

```c
#include<stdio.h>
typedef struct
{
    int dan;
    int mesec;
    int godina;
} Datum;

typedef struct
{
    char prezime[20];
    char ime[20];
    Datum dat_rodj;
    int god_studija;
    float prosecna_ocena;
} Student;

int main(void)
{
    Student std,*p;
    p = &std;
    printf("Unesi ime studenta: ");
    gets(p->ime);
    printf("Unesi prezime studenta: ");
    gets(p->prezime);
    printf("Unesi datum rodjenja: ");
    scanf("%d", p->dat_rodj.dan);
    printf("Unesi mesec rodjenja: ");
    scanf("%d", p->dat_rodj.mesec);
    printf("Unesi godinu rodjenja: ");
    scanf("%d", p->dat_rodj.godina);
    printf("Unesi godinu studija: ");
    scanf("%d", p->god_studija);
    printf("Unesi prosecnu ocenu : ");
    scanf("%f", p->prosecna_ocena);
    printf("Uneli ste studenta\n");
    printf("Ime i prezime: %s %s\n", p->ime, p->prezime);
    printf("Datum rodjenja %d.%d.%d\n", p->dat_rodj.dan, p->dat_rodj.mesec, p->dat_rodj.godina);
    printf("Godina studija %d\n", p->god_studija);
    printf("Prosecna ocena %.2f\n", p->prosecna_ocena);
    return 0;
}
```

```{questionnote}
Дефинисати структурни тип `Tacka` са пољима `x`, `y` типа `float`. У
главном програму дефинисати показивачку променљиву `p` типа `Tacka` и
резервисати меморијски простор за један податак типа `Tacka`. Унети и исписати
једну тачку користећи показиваче.
```

```c
#include<stdio.h>
#include<malloc.h>
typedef struct
{
    float x;
    float y;
} Tacka;

int main(void)
{
    Tacka *p = (Tacka*) malloc(sizeof(Tacka));
    printf("Unesi x koordinatu:");
    scanf("%f",&p->x);
    printf("Unesi y koordinatu:");
    scanf("%f",&p->y);
    printf("(%.2f, %.2f)\n", p->x, p->y);
    free(p);	
    return 0;
}
```

Излаз:

```text
Unesi x koordinatu: 3.25
Unesi y koordinatu: 2.89
(3.25, 2.89)
```
