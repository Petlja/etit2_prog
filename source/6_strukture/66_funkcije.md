# Структуре и функције

Као што смо раније нагласили, над структуром се могу применити следеће
операције:

- копирање и додела вредности,
- узимање адресе структуре оператором `&` (операције над структуром као
целином), или обраћање члановима структуре.

Зато се структуре могу појавити као аргументи функције, односно као вредност
коју функција враћа.

Структуре се не могу поредити, али се могу поредити поља структуре.

Структуре као аргументи функције могу се преносити као целине, преносом
компоненти или преносом адресе структуре (показивача на структуру).

Вредност функције такође може бити типа структуре или показивача на структуру.

```{questionnote}
Дефинишите структурни тип `Tacka` који се састоји од два поља `x`, `y`
типа `int`. Написати следеће функције:

- функцију `postavi_tacku` којој су улазни параметри координате тачке `x` и `y` типа
`int` и чија је повратна вредност структурног типа `Tacka`
- функцију `saberi_koordinate` којој су улазни параметри две структурне променљиве `Т1` и
`Т2` типа `Tacka` и која рачуна збир координата тих тачака по x односно y оси. Повратна вредност функције је структурног типа `Tacka`
- функцију `ispisi_tacku` без повратне вредности која исписује координате тачке
у облику `(x,y)`

Написати програм којим се уносе координате две тачке, врши сабирање x и y координата истих и приказује вредост координата нове тачке.
```
**Решење:**

```c
#include<stdio.h>
typedef struct {
    int x;
    int y;
} Tacka;

Tacka postavi_tacku(int x,int y)
{
    Tacka T;
    T.x = x;
    T.y = y;
    return T;
}

Tacka saberi_koordinate(Tacka T1,Tacka T2)
{
    Tacka T;
    T.x = T1.x + T2.x;
    T.y = T1.y + T2.y;
    return T;
}

void ispisi_tacku(Tacka T)
{
    printf("(%d, %d)", T.x, T.y);
}
int main(void)
{
    int x, y;
    Tacka A, B, C;
    printf("Unesi x koordinatu tacke A: ");
    scanf("%d", &x);
    printf("Unesi y koordinatu tacke A: ");
    scanf("%d", &y);
    A = postavi_tacku(x, y);
    printf("Unesi x koordinatu tacke B: ");
    scanf("%d", &x);
    printf("Unesi y koordinatu tacke B: ");
    scanf("%d", &y);
    B = postavi_tacku(x, y);
    printf("\nUneli ste tacke \n");
    printf("A");
    ispisi_tacku(A);
    printf("\nB");
    ispisi_tacku(B);
    C = saberi_koordinate(A,B);
    printf("\nNakon sabiranja x i y koordinata tacaka A i B dobija se tacka C");
    ispisi_tacku(C);
    return 0;
}
```

Излаз:

```text
Unesi x koordinatu tacke A: 2
Unesi y koordinatu tacke A: 3
Unesi x koordinatu tacke B: 7
Unesi y koordinatu tacke B: 2

Uneli ste tacke
A(2, 3)
B(7, 2)

Nakon sabiranja x i y koordinata tacaka A i B dobija se tacka C(9,5)
```

```{questionnote}
Дефинишите структурни тип `Tacka` који се састоји од два поља `x`, `y`
типа `int`. Написати следеће функције:

- функцију `rastojanje` којој су улазни параметри две структурне променљиве `Т1` и
`Т2` типа `Tacka`. Функција рачуна растојање између тих тачака у координатном систему. Повратна вредност функције је реалног типа.
- функцију `najbliza` којој су улазни параметри низ тачака структурног типа `Tacka` и број унетих тачака. Повратна вредност функције је показивач на тачаку која је најближа координатном почетку.

Написати програм којим се уноси низ тачака и којим се одређује и приказује тачка  која је најближа координатном почетку NULA(0,0). 
```

**Решење**:

```c
#include<stdio.h>
#include<math.h>
typedef struct {
    int x;
    int y;
} Tacka;
const Tacka NULA = {0, 0};

double rastojanje(Tacka A, Tacka B)
{
    return sqrt(pow(A.x - B.x,2) + pow(A.y - B.y,2));
}

Tacka *najbliza (Tacka T[], int n)
{
    Tacka *min = T;
    double r = rastojanje(T[0], NULA);
    int i;
    for (i = 1; i < n; i++)
    {
        double s = rastojanje(T[i], NULA);
        if (s<r)
        { 
            r= s;
            min = T + i;
        }
        return min;
    }
}

int main(void)
{
    Tacka niz[10], *p;
    int i, n;
    printf("Unesi broj tacaka < 11: ");
    scanf("%d", &n);
    for(i = 0; i < n; i++)
    {
        printf("Unesi x koordinatu tacke %d: ", i + 1);
        scanf("%d", &niz[i].x);	
        printf("Unesi y koordinatu tacke %d: ",i + 1);
        scanf("%d", &niz[i].y);		
    }
    p = najbliza(niz, n);
    printf("Tacka sa koordinatama %d i %d je najbliza koordinatnom pocetku", p->x, p->y);
    return 0;
}
```

Излаз:

```text
Unesi broj tacaka < 11: 4
Unesi x koordinatu tacke 1: 1
Unesi y koordinatu tacke 1: 1
Unesi x koordinatu tacke 2: 0
Unesi y koordinatu tacke 2: 1
Unesi x koordinatu tacke 3: 2
Unesi y koordinatu tacke 3: 2
Unesi x koordinatu tacke 4: 3
Unesi y koordinatu tacke 4: 2
Tacka sa koordinatama 0 i 1 je najbliza koordinatnom pocetku
```
