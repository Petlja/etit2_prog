# Функције и матрице

Хајде да се подсетимо.

Код преноса вредности низа у функцију користили смо референцу низа. Погледајмо
пример функције за унос и испис једнодимензионалног низа.

```c
#include<stdio.h>
void unos_niz(int b[], int n)
{
    int i;
    for (i = 0; i < n; i++)
    {
        printf("a[%d] = ",i);
        scanf("%d", &b[i]);
    }
}

void ispis_niz(int b[],int n)
{
    int i;
    for(i = 0; i < n; i++)
        printf("a[%d] = %d\n", i, b[i]);
}

int main(void)
{
    int a[10], i, n;
    printf("Unesite broj elemenata niza: ");
    scanf("%d",&n);
    printf("Unesite niz:\n");
    unos_niz(a, n);
    printf("\nUneli ste elemente niza: \n");
    ispis_niz(a, n);
    return 0;	
}
```

Излаз:

```text
Unesite broj elemenata niza: 6
Unesite niz:
a[0] = 1
a[1] = 2
a[2] = 3
a[3] = 4
a[4] = 5
a[5] = 6

Uneli ste elemente niza:
a[0] = 1
a[1] = 2
a[2] = 3
a[3] = 4
a[4] = 5
a[5] = 6
```

Као први параметар, функцији прослеђујемо низ преко адресе, а као други
параметар број елемената преко вредности. Примећујемо да није неопходно у низу
`b` у функцији резервисати број места у угластој загради. Практично, када се
спољашња вредност низа `a` пренесе функцијској променљивој, пренесе се и
резервисан простор из спољашњег низа.

Такође примећујемо да је приликом позива функције довољно само навести
идентификатор низа. У суштини, функцијској променљивој `b` се додељује адреса
спољашњег низа `a`.

Да видимо како бисмо написали функцију за унос матрице.

```c
void unos_2d_niz(int B[][50],int n, int m)
{
    int i, j;
    for (i = 0; i < n; i++)
        for (j = 0; j < m; j++)
        {
            printf("A[%d][%d] = ",i,j);
            scanf("%d", &B[i][j]);
        } 
}
```

Сада да напишемо функцију за испис матрице.

```c
void ispis_2d_niz(int B[][50], int n, int m)
{
    int i, j;
    for (i = 0; i < n; i++)
    {
        for (j = 0; j < m; j++)
            printf("%6d]", B[i][j]);
    printf("\n");
    }
}
```

```{questionnote}
Шта примећујемо? 
```

Функцији морамо да проследимо димензију матрице. Видимо да
број резервисаних редова не мора да се унесе, док је број елемената у реду
обавезан податак. То је зато што компајлер мора да зна одакле ће се у меморији
позиционирати следећи ред, док је број редова ограничен капацитетом меморије.

```{questionnote}
Написати програм за унос и испис матрице целобројног типа елемената,
максималних димензија 50х50 и димензија `r` х `k`, користећи функције.
```

**Решење**:

```c
#include<stdio.h>
void unos_2d_niz(int B[][50],int n, int m);
void ispis_2d_niz(int B[][50],int n, int m);
int main(void)
{
    int A[50][50], r, k;
    printf("Unesite broj redova: ");
    scanf("%d", &r);
    printf("Unesite broj kolona: ");
    scanf("%d", &k);
    printf("Unesite elemente matrice:\n");
    unos_2d_niz(A, r, k);
    printf("\nUneli ste elemente matrice: \n");	
    ispis_2d_niz(A, r, k);
    return 0;
}

void unos_2d_niz(int B[][50],int n, int m)
{
    int i,j;
    for (i = 0; i < n; i++)
        for (j = 0; j < m; j++)
        {
            printf("A[%d][%d] = ", i, j);
            scanf("%d", &B[i][j]);
        } 
}

void ispis_2d_niz(int B[][50], int n, int m)
{
    int i, j;
    for (i = 0; i < n; i++)
    {
        for (j = 0; j < m; j++)
            printf("%6d", B[i][j]);
        printf("\n");
    }
}
```

Излаз:

```text
Unesite broj redova: 4
Unesite broj kolona: 3
Unesite elemente matrice:
B[0][0] = 1
B[0][1] = 2
B[0][2] = 3
B[1][0] = 4
B[1][1] = 5
B[1][2] = 6
B[2][0] = 7
B[2][1] = 8
B[2][2] = 9
B[3][0] = 10
B[3][1] = 11
B[3][2] = 12

Uneli ste elemente matrice:
     1     2     3
     4     5     6
     7     8     9
    10    11    12
```
```{questionnote}
Написати програм за унос `n` елемената матрице од максимално 50х50
елемената. Подаци су реалног типа података. Израчунати и исписати на излазу
збир елемената главне дијагонале.
```

**Решење**:

```c
#include<stdio.h>
void unos_2d_niz(float B[][50], int n);
void ispis_2d_niz(float B[][50], int n);
float zbir_glavna(float B[][50], int n);
int main(void)
{
    float A[50][50];
    int n;
    printf("Unesite broj redova/kolona ");
    scanf("%d", &n);
    printf("Unesite elemente matrice\n");
    unos_2d_niz(A, n);
    printf("\nUneli ste elemente matrice: \n");
    ispis_2d_niz(A, n);
    printf("\nZbir elemenata glavne dijagonale je %.2f", zbir_glavna(A, n));
    return 0;
}

void unos_2d_niz(float B[][50], int n)
{
    int i, j;
    for (i = 0; i < n; i++)
        for (j = 0; j < n; j++)
        {
            printf("A[%d][%d] = ", i, j);
            scanf("%f", &B[i][j]);
        } 
}

void ispis_2d_niz(float B[][50], int n)
{
    int i, j;
    for(i = 0; i < n; i++)
    {
        for (j = 0; j < n; j++)
            printf("%6.2f", B[i][j]);
        printf("\n");
    }
}

float zbir_glavna(float B[][50], int n)
{
    int i, j;
    float s = 0;
    for(i = 0; i < n; i++)
        for (j = 0; j < n; j++)
            if(i == j)
                s = s + B[i][j];	
	return s;
}
```

Излаз:

```text
Unesite broj redova/kolona: 3
Unesite elemente matrice:
A[0][0] = 1.256
A[0][1] = 2.358
A[0][2] = 3.12
A[1][0] = 1.25
A[1][1] = 3.00
A[1][2] = 4
A[2][0] = 5.2469
A[2][1] = 11.25
A[2][2] = 12.253

Uneli ste elemente matrice:
  1.26  2.36  3.12
  1.25  3.00  4.00
  5.25 11.25 12.25

Zbir elemenata glavne dijagonale je 16.51
```

```{questionnote}
За матрицу која се састоји од реалних бројева написати модул `niz.h`
који ће садржати функције за…
```

- унос елемената матрице
- испис елемената матрице
- испис елемената главне дијагонале
- испис елемената споредне дијагонале
- испис елемената троугла изнад главне дијагонале
- испис елемената троугла испод главне дијагонале
- испис елемената троугла изнад споредне дијагонале
- испис елемената троугла испод споредне дијагонале
- израчунавање збира елемената матрице
- израчунавање збира елемената главне дијагонале матрице
- израчунавање збира елемената споредне дијагонале матрице
- израчунавање збира елемената троугла изнад главне дијагонале матрице
- израчунавање збира елемената троугла испод главне дијагонале матрице
- израчунавање збира елемената троугла изнад споредне дијагонале матрице
- израчунавање збира елемената троугла испод споредне дијагонале матрице
- одређивање максималног елемента матрице
- одређивање минималног елемента матрице


```{questionnote}
Користећи модул `niz.h` написати програм за рад са матрицом реалних
бројева. Креирати мени за избор функције. У случају да се захтева да унета
матрица мора да буде квадратна (функције за рад са дијагоналама), а број редова
се разликује од броја колона, исписати поруку: „Матрица није квадратна. Број
редова и колона мора бити исти.“ За проверу да ли је матрица квадратна
користити функцију `provera(r, k)` која враћа логичку повратну вредност, где су
параметри број редова односно колона.
```

На Петљи можете решавати задатке из Методичке збирке задатака из основа
програмирања, део Матрице, који се налазе на линку
[Metodicka zbirka zadataka](https://petlja.org/biblioteka/r/Zbirka/04%20Nizovi/03%20visedimenzionalni/01%20matrice),
користећи онлајн С или С/С++ компајлер.

За почетак пробајте да решите задатак из збирке који се налази на линку
[Sortiranje po proseku](https://petlja.org/biblioteka/r/Zbirka/sortiranje_po_proseku).
