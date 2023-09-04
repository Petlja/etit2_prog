# Приступ елементима матрице – унос и испис елемената

Приступ појединим елементима матрице врши се навођењем индекса у угластој
загради. Хајде да напишемо програм којим ћемо унети једну матрицу `А` целих
бројева, димензија два реда и две колоне, и након тога исписати унете елементе.

Решење:

```c
#include<stdio.h>
int main(void)
{
    int A[2][2];
    printf("Unesi element A[0][0]: ");
    scanf("%d",&A[0][0]);
    printf("Unesi element A[0][1]: ");
    scanf("%d",&A[0][1]);
    printf("Unesi element A[1][0]: ");
    scanf("%d",&A[1][0]);
    printf("Unesi element A[1][1]: ");
    scanf("%d",&A[1][1]);
    printf("\nUneli ste matricu:");
    printf("\nA[0][0] = %d", A[0][0]);
    printf("\nA[0][1] = %d", A[0][1]);
    printf("\nA[1][0] = %d", A[1][0]);
    printf("\nA[1][1] = %d", A[1][1]);
    return 0;
}
```

Излаз:

```text
Unesi element A[0][0]: 6
Unesi element A[0][1]: 4
Unesi element A[1][0]: 8
Unesi element A[1][1]: 7

Uneli ste matricu:
A[0][0] = 6
A[0][1] = 4
A[1][0] = 8
A[1][1] = 7
```

Видимо да је потребно више пута написати наредбе за унос и испис појединих
елемената. Хајде да направимо програм којим ћемо уносити елемент по елемент.

```{questionnote}
Написати програм за унос и испис елемената матрице целобројног типа
елемената од 3 реда (врсте) и 4 колоне (димензије 3 х 4).
```

**Решење**:

```c
#include<stdio.h>
int main(void)
{
    int A[3][4], i, j;
    printf("Unesite elemente matrice:\n");
    for(i = 0; i < 3; i++)
        for (j = 0; j < 4; j++)
        {
            printf("A[%d][%d] = ", i, j);
            scanf("%d", &A[i][j]);
        }
    printf("\nUneli ste matricu: \n");
    for(i = 0; i < 3 ; i++)
        for (j = 0; j < 4; j++)
            printf("A[%d][%d] = %d\n", i, j, A[i][j]);
    return 0;
}
```

Излаз:

```text
Unesite elemente matrice:
A[0][0] = 1
A[0][1] = 2
A[0][2] = 3
A[0][3] = 4
A[1][0] = 5
A[1][1] = 6
A[1][2] = 7
A[1][3] = 8
A[2][0] = 9
A[2][1] = 10
A[2][2] = 11
A[2][3] = 12

Uneli ste matricu:
A[0][0] = 1
A[0][1] = 2
A[0][2] = 3
A[0][3] = 4
A[1][0] = 5
A[1][1] = 6
A[1][2] = 7
A[1][3] = 8
A[2][0] = 9
A[2][1] = 10
A[2][2] = 11
A[2][3] = 12
```

Шта можете да приметите у уносу? Користили смо угнежђену петљу. Прво смо унели
све елементе првог реда, а након тога елементе другог реда. Значи, уносили смо
елементе матрице по редовима.

```{image} images/image12.png
:width: 350
:align: center
```

```{image} images/image13.png
:width: 350
:align: center
```

```{questionnote}
Шта треба да се промени у програму да се изврши уношење елемената по
колонама?
```

**Одговор**: Треба заменити места циклусима. Спољашњи циклус треба да се мења по
`j`, а унутрашњи по `i`.

```{questionnote}
Написати програм за унос и испис елемената матрице целобројног типа
елемената димензија 3х4 и графички приказати пролазак кроз матрицу, као у
претходном примеру.
```

**Решење**:

```c
#include<stdio.h>
int main(void)
{
    int A[3][4], i, j;
    printf("Unesite elemente matrice:\n");
    for(j = 0; j < 4; j++)
        for (i = 0; i < 3; i++)
        {
            printf("A[%d][%d] = ",i,j);
            scanf("%d",&A[i][j]);
        }
    printf("\nUneli ste matricu:\n");
    for(i = 0; i < 3; i++)
        for (j = 0; j < 4; j++)
            printf("A[%d][%d] = %d\n", i, j, A[i][j]);
    return 0;
}
```

Излаз:

```text
Unesite elemente matrice:
A[0][0] = 1
A[1][0] = 5
A[2][0] = 9
A[0][1] = 2
A[1][1] = 6
A[2][1] = 10
A[0][2] = 3
A[1][2] = 7
A[2][2] = 11
A[0][3] = 4
A[1][3] = 8
A[2][3] = 12

Uneli ste matricu:
A[0][0] = 1
A[0][1] = 2
A[0][2] = 3
A[0][3] = 4
A[1][0] = 5
A[1][1] = 6
A[1][2] = 7
A[1][3] = 8
A[2][0] = 9
A[2][1] = 10
A[2][2] = 11
A[2][3] = 12
```

```{image} images/image14.png
:width: 350
:align: center
```

```{image} images/image15.png
:width: 350
:align: center
```

```{questionnote}
Написати програм за унос и испис матрице целобројног типа елемената
максималних димензија 10х10 и димензија `r` х `k`, као и за приказ унете матрице
ред по ред.
```

**Решење**:

```c
#include<stdio.h>
int main(void)
{
    int A[10][10], i, j, r, k;
    printf("Unesite broj redova: ");
    scanf("%d", &r);
    printf("Unesite broj kolona: ");
    scanf("%d", &k);
    printf("Unesite elemente matrice:\n");
    for (i = 0; i < r; i++)
        for (j = 0; j < k; j++)
        {
            printf("A[%d][%d] = ", i, j);
            scanf("%d", &A[i][j]);
        }
    printf("\nUneli ste matricu:\n");
    for (i = 0; i < r; i++){
        for (j = 0; j < k; j++)
            printf("%6d", A[i][j]);
        printf("\n");
    }
    return 0;
}
```

Излаз:

```text
Unesite broj redova: 3
Unesite broj kolona: 4
Unesite elemente matrice:
A[0][0] = 1
A[0][1] = 2
A[0][2] = 3
A[0][3] = 4
A[1][0] = 5
A[1][1] = 6
A[1][2] = 7
A[1][3] = 8
A[2][0] = 9
A[2][1] = 10
A[2][2] = 11
A[2][3] = 12

Uneli ste matricu:
1	2	3	4
5	6	7	8
9	10	11	12
```

```{questionnote}
Шта смо променили у програму да би се сваки ред исписивао у новом реду?
```

**Одговор**: Након другог циклуса додали смо пребацивање у нови ред. Други циклус
смо ставили у блок и на крају блока додали пребацивање у нови ред.
