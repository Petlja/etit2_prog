# Сажимање низова

Сажимање представља избацивање појединих чланова низа и формирање новог низа

```{questionnote}
Иницијализујте један низ од шест целобројних елемената a[6]={1, 5, 3, 2, 4, 6}.
Сажмите низ тако што ћете избацити елементе који имају вредност ``izbaci = 2``. На основу
циклуса за сажимање написати  програм.
```

```{image} images/Picture60.png
:width: 35%
:align: center
```

Решење:

```c
#include <stdio.h> 
main() 
{ 
	int a[6]={1,5,3,2,4,6},i,j,izbaci,n,k=0;;
	printf("\nUneti niz:\n"); 
	for(i=0;i<6;i++) 
	{ 
    		printf("a[%d]=%d\n",i,a[i]); 
	}
	printf("Unesite elemenat koji izbacujete: ");
	scanf("%d",&izbaci);
	for (int i=0; i<6; i++)
	{
    		if (a[i] != izbaci)
        		a[k++] = a[i];
	}
	n=k;
	printf("\nSazet niz izgleda izgleda :\n");
	for(j=0;j<n;j++) 
	{ 
    		printf("a[%d]=%d\n",j,a[j]); 
	}
}
```

Излаз:

```text
Uneti niz:
a[0]=1
a[1]=5
a[2]=3
a[3]=2
a[4]=4
a[5]=6
Unesite elemenat koji izbacujete: 2

Sazet niz izgleda izgleda :
a[0]=1
a[1]=5
a[2]=3
a[3]=4
a[4]=6
```

Хајде да анализирамо шта се налази у циклусу означеним бројем 1. Унели смо да
се избацује елемент izbaci =  2.

```{image} images/Picture61.png
:width: 50%
:align: center
```

Следећи корак i=i+1

```{image} images/Picture62.png
:width: 50%
:align: center
```

Следећи корак i=i+1

```{image} images/Picture63.png
:width: 50%
:align: center
```

Следећи корак i=i+1

```{image} images/Picture64.png
:width: 50%
:align: center
```

Следећи корак i=i+1

```{image} images/Picture65.png
:width: 50%
:align: center
```

Следећи корак i=i+1

```{image} images/Picture66.png
:width: 50%
:align: center
```

Следећи корак i=i+1=6 . For циклус је достигао граничну вредност и прекида се

Пошто је  je n=k, n=5 на крају је остао низ

```{image} images/Picture67.png
:width: 35%
:align: center
```

Задатак: Написати програм којим се уноси n елемената целобројног низа, а затим
врши избацивање жељеног елемента. Предвидети да уколико се унесе вредност која се
не налази у низу испише поруку "У низу не постоји елемент за избацивање". Уколико је
све у реду исписати сажети низ.

Решење:

```c
#include <stdio.h> 
main() 
{
	int i,a[50],n,izbaci,k=0;
	printf("Unesi koliko elemenata niza unosis ");
	scanf("%d",&n);
	printf ("Unesi %d elemenata niza: \n",n);
	for (i=0; i<n; i++)
	{ 
  		printf ("a[%d]=",i);
		scanf ("%d",&a[i]);
	}
	printf("Unesite elemenat koji izbacujete: ");
	scanf("%d",&izbaci);
	for (int i=0; i<n; i++)
	{
    		if (a[i] != izbaci)
        		a[k++] = a[i];
	}
	if(n==k)
	{
		printf("\nU nizu ne postoji element za izbacivanje");
		printf("\nNiz je ostao nepromenjen\n");
	for(i=0;i<n;i++) 
	{ 
  		printf("a[%d]=%d\n",i,a[i]); 
	}
	}
	else
	{
		n=k;
		printf("\nSazet niz izgleda izgleda :\n");
		for(i=0;i<n;i++) 
		{ 
  			printf("a[%d]=%d\n",i,a[i]); 
		}	
	}
}
```

Ако се тражени елементи налазе у низу на излазу се добија:

```text
Unesi koliko elemenata niza unosis 6
Unesi 6 elemenata niza:
a[0]=5
a[1]=2
a[2]=2
a[3]=8
a[4]=9
a[5]=5
Unesite elemenat koji izbacujete: 5
Sazet niz izgleda izgleda :
a[0]=2
a[1]=2
a[2]=8
a[3]=9
```

Ако се тражени елементи не налазе у низу на излазу се добија:

```text
Unesi koliko elemenata niza unosis 6
Unesi 6 elemenata niza:
a[0]=5
a[1]=2
a[2]=2
a[3]=8
a[4]=9
a[5]=5
Unesite elemenat koji izbacujete: 1
U nizu ne postoji element za izbacivanje
Niz je ostao nepromenjen
a[0]=5
a[1]=2
a[2]=2
a[3]=8
a[4]=9
a[5]=5
```
