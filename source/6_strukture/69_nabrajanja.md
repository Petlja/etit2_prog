# Набрајања – enum

Набројиве константе су целобројне симболичке константе којима су вредности
додељене експлицитно или имплицитно набрајањем њихових имена у низу.

Општи облик набрајања би био:

```text
enum ime_nabrajanja { ime_konstante = vrednost, 
                 ....			
            ime_konstante = vrednost};
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
- набројиви тип:

```c
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

Промењивој `boja` била би додељена вредност `PLAVA`.

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

Пример програма за набрајање
```c
#include <stdio.h>
enum dani
{
    Pon,Uto,Sre,Cet,Pet,Sub,Ned
};
main()
{
    enum dani danas=Sre;
    if(danas==6||danas==7)//Ovde moze biti i uslov  if(danas==Sub||danas==Ned)
    {
        printf("Dana nije radni dan ");
    }	
    else 
    {
        printf("Danas se radi ");
    }	
}
```

