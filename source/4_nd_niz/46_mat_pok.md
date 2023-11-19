# Матрице и показивачи

Оперативна меморија је по природи једнодимензионално поље, па се матрице
смештају по редовима (врстама) – прва врста на почетку, иза ње друга...

## Динамичко формирање матрице

Посматрајмо један дводимензионални низ `А` од целих бројева, димензија 3 х 4.

```{image} images/image19.png
:width: 500
:align: center
```

Обратите пажњу да је овде назив низа у ствари адреса првог елемента у матрици. Као
што смо на почетку рекли, матрица се може посматрати као низ низова. Можете видети на слици да ако се показивачка промењива `А` повећа за `1` неће се прећи на следећи елемент првог реда, већ ће се показивач померити на адресу првог елемента наредног реда. 

Матрица се може динамички дефинисати тако што се оформи статички низ показивача
од којих сваки показује на један од компонентних низова (тј. на један ред или
колону матрице). На пример наредбом `&A[i][j] = A[i]+j = *(А + i) + j` приступа се адреси елемента у реду са индексом `i` и колони са индексом `j`, односно наредбом `A[i][j] = *(A[i]+j)= *(*(А + i) + j)` добијамо вредност елемента на истој позицији.

```{image} images/image20.png
:width: 500
:align: center
```

```{questionnote}
Формирати целобројну матрицу `А` од 4 врсте и 10 колона (матрица се
састоји од узастопних бројева) помоћу 4 независна низа од по 10 компоненти у
динамичкој зони меморије.
```

```{image} images/image21.png
:width: 500
:align: center
```

**Решење**:

```c
#include<stdio.h>
#include<stdlib.h>
int main(void) {
    int **A, i, j; //matricu deklarisemo kao pokazivac na pokazivac **a
    A = (int**)calloc(4,sizeof(int*));//pokazivacu a se dodeljuje prostor za smestanje niza od 4 pokazivaca
    for(i = 0; i < 4; i++) 
    {
        *(A+i) = (int*)calloc(10, sizeof(int*));//za svaku vrstu se rezervise prostor za 10 elemenata te vrste
        for(j = 0; j < 10; j++) 
        {
            *(*(A + i) +j) = 10 * i + j;
            printf("%5d", *(*(A + i) +j));
        }
        printf("\n");
    }
    free(A);
    return 0;
}
```

Излаз:

```text
    0    1    2    3    4    5    6    7    8    9
   10   11   12   13   14   15   16   17   18   19
   20   21   22   23   24   25   26   27   28   29
   30   31   32   33   34   35   36   37   38   39
```

```{questionnote}
Формирати целобројну матрицу `А` од `r` редова (врста) и `k` колона
(матрица се састоји од узастопних бројева) помоћу `r` независних низова од по
`k` компоненти у динамичкој зони меморије.
```

**Решење**:

```c
#include<stdio.h>
#include<stdlib.h>
int main(void) {
    int **A, i, j, r, k; //matricu deklarisemo kao pokazivac na pokazivac **a
    printf("Broj redova: "); 
    scanf("%d", &r);
    printf("Broj kolona: ");
    scanf("%d", &k);
    A = (int**)calloc(r,sizeof(int*));//pokazivacu a se dodeljuje prostor za smestanje niza od r pokazivaca
    for (i = 0; i < r; i++) 
    {
    *(A + i) = (int*)calloc(k, sizeof(int*));//za svaku vrstu se rezervise prostor za k elemenata te vrste
        for (j = 0; j < k; j++) 
        {
            *(*(A + i) + j) = k * i + j;
            printf("%5d", *(*(A + i) + j));
        }
        printf("\n");
    }
    free(A);
    return 0;
}
```

Излаз:

```text
Broj redova: 4
Broj kolona: 6
    0    1    2    3    4    5
    6    7    8    9   10   11
   12   13   14   15   16   17
   18   19   20   21   22   23
```

```{questionnote}
Формирати целобројну матрицу `А` од `r` редова (врста) и `k` колона
(матрица се састоји од узастопних бројева) помоћу `r` независних низова од по
`k` компоненти у динамичкој зони меморије. На излазу исписати изглед матрице и
адресе одговарајућих елемената.
```

**Решење**:

```c
#include <stdio.h>
#include <stdlib.h>
int main(void)
{
    int **A, i, j, r, k; //matricu deklarisemo kao pokazivac na pokazivac **a
    printf("Broj redova: "); 
    scanf("%d", &r);
    printf("Broj kolona: ");
    scanf("%d", &k);
    A = (int**)calloc(r,sizeof(int*));//pokazivacu a se dodeljuje prostor za smestanje niza od r pokazivaca
    for (i = 0; i < r; i++) 
    {
        *(A + i) = (int*)calloc(k, sizeof(int*));//za svaku vrstu se rezervise prostor za k elemenata te vrste
        for (j = 0; j < k; j++) 
        {
            *(*(A + i) + j) = k * i + j;
            printf("%5d", *(*(A + i) + j));
        }
        printf("\n");
    }
     printf("\nAdrese elemenata matrice su:\n");
    for (i = 0; i < r; i++)
    {
        for(j = 0; j < k; j++)
            printf("A[%d][%d] = %x\n", i, j, (*(A + i) + j));
        printf ("\n");
    }
    for (int i = 0; i < r; i++)
    free(*(A + i));//oslobadja se rezervisan memorijski prostor za svaki red
    free(A);//oslobadja se rezervisan memorijski prostor za prvi elemenat matrice
    return 0;
}
```

Излаз:

```text
Broj redova: 3
Broj kolona: 4
    0    1    2    3
    4    5    6    7
    8    9   10   11

Adrese elemenata matrice su:
A[0][0] = b31440
A[0][1] = b31444
A[0][2] = b31448
A[0][3] = b3144c

A[1][0] = b31470
A[1][1] = b31474
A[1][2] = b31478
A[1][3] = b3147c

A[2][0] = b314a0
A[2][1] = b314a4
A[2][2] = b314a8
A[2][3] = b314ac
```

## Зупчаста матрица

Формирање матрице на претходно приказан начин омогућава да компоненте низова
(редови) могу да буду променљиве дужине, а њихове величине се одређују у време
извршења програма. Тако формирана матрица назива се зупчаста матрица.
Представимо то у меморији.

```{image} images/image22.png
:width: 400
:align: center
```

Како код зупчасте матрице број колона није исти у сваком реду (врсти), морамо
за сваки ред (врсту) да памтимо колико она има елемената.

Поставља се питање где сачувати податак о броју колона у реду. Најједноставније
је да у првом елементу (индекс 0) сваког реда (врсте) памтимо дужину тог реда,
односно број колона, а од позиције 2 (индекс 2) до позиције `k+1` (индекс `k`)
памтимо саме елементе тог реда.

```{questionnote}
Написати програм за унос зупчасте матрице `А`, а затим приказати унету
матрицу.
```  

**Решење**:

```c
#include<stdio.h>
#include<stdlib.h>
int main(void) 
{
    int **A, i, j, r, k; //matricu deklarisemo kao pokazivac na pokazivac **a
    printf("Broj redova: " ); 
    scanf("%d", &r);
    A = (int**)calloc(r, sizeof(int*)); //pokazivacu A se dodeljuje prostor za smestanje niza od r pokazivaca
    for(i = 0; i < r; i++) 
    {
    printf("\nBroj kolona u %d. redu: ", i + 1);
    scanf("%d",&k);
    *(A + i) = (int*)calloc(k + 1, sizeof(int*));//za svaki red se rezervise prostor za k elemenata tog reda +1 
    A[i][0] = k; //na pocetnoj poziciji reda pamtimo duzinu tog reda
    printf("Unesite elemente %d. reda:\n",i + 1);
        for(j = 1; j < k + 1; j++) 
        {	
            printf("A[%d][%d] = ", i, j);
            scanf("%d", &A[i][j]);
        }
    }
    printf("Uneli ste matricu: \n");
    for(i = 0; i < r; i++)
    {
        k = A[i][0];// citamo broj kolona u i-tom redu
        for(j = 1; j < k + 1; j++) 	
            printf("%6d", A[i][j]);
    printf("\n");
    }
    return 0;
}
```

Излаз:

```text
Broj redova: 3

Broj kolona u 1. redu: 3
Unesi elemente 1. reda:
A[0][1] = 1
A[0][2] = 2
A[0][3] = 3

Broj kolona u 2. redu: 4
Unesi elemente 2. reda:
A[1][1] = 4
A[1][2] = 5
A[1][3] = 6
A[1][4] = 7

Broj kolona u 3. redu: 1
Unesi elemente 3. reda:
A[2][1] = 8
Uneli ste matricu:
     1     2     3
     4     5     6     7
     8 
```