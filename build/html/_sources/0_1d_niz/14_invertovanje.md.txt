# Инвертовање низова

Инвертовање представља замену чланова низа тако да први постане задњи, други
предзадњи тако редом. Постоје два начина

- без увођења новог низа
- уз увођење новог низа

Погледајмо како изгледа циклус за инвертовање без увођење новог низа

```{image} images/Picture40.png
:width: 30%
:align: center
```

Задатак: Иницијализујте један низ од шест целобројних елемената a[6]={1,5,3,2,4,6}.
На основу горњег циклуса написати програм за инвертовање.

Решење:

```c
#include <stdio.h> 
main() 
{ 
	int a[6]={1,5,3,2,4,6},b,i,j; 
	printf("\nUneti niz:\n"); 
	for(i=0;i<6;i++) 
	{ 
    		printf("a[%d]=%d\n",i,a[i]); 
	} 
	for (i=0, j=5; i<j; i++, j--) 
	{ 
     		b=a[i]; a[i]=a[j]; a[j]=b; 
	} 
	printf("\nInvertovani niz :\n");
	for(i=0;i<6;i++) 
	{ 
    		printf("a[%d]=%d\n",i,a[i]); 
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

Invertovani niz :
a[0]=6
a[1]=4
a[2]=2
a[3]=3
a[4]=5
a[5]=1
```

Хајде да анализирамо корак по корак шта се дешава кроз циклус

Промењива b нам служи да привремено сачувамо вредност низа коју
замењујено другом вредношћу.

```{image} images/Picture41.png
:width: 70%
:align: center
```

```{image} images/Picture42.png
:width: 70%
:align: center
```

```{image} images/Picture43.png
:width: 70%
:align: center
```

Приметићете да у овом случају нисмо уводили нови низ.

Задатак : Иницијализујте један низ од шест целобројних елемената a[6]={1,5,3,2,4,6}.
Пробајте да направите програм за инвертовање низа уз увођење новог низа користећи
циклус

```{image} images/Picture44.png
:width: 70%
:align: center
```

Решење:

```c
#include <stdio.h> 
main() 
{ 
	int a[6]={1,5,3,2,4,6},b[6],i,j; 
	printf("\nUneti niz:\n"); 
	for(i=0;i<6;i++) 
	{ 
    	printf("a[%d]=%d\n",i,a[i]); 
	} 
	for(i=0; i<6; i++)
      		b[5-i]= a[i];
	printf("\nInvertovani niz :\n");
	for(i=0;i<6;i++) 
	{ 
    		printf("a[%d]=%d\n",i,b[i]); 
	}
}
```

Добија се идентичан излаз као и без увођења новог низа

У овом случају ћемо један по један елемент из низа а уносити у низ b. Први
члан низа а пресликавамо у последњи низа b. Други члан низа а пресликавамо
у претпоследњи низа b. И тако редом.

Хајде да анализирамо корак по корак шта се дешава кроз циклус

```{image} images/Picture45.png
:width: 70%
:align: center
```

```{image} images/Picture46.png
:width: 70%
:align: center
```

```{image} images/Picture47.png
:width: 70%
:align: center
```

```{image} images/Picture48.png
:width: 70%
:align: center
```

```{image} images/Picture49.png
:width: 70%
:align: center
```

```{image} images/Picture50.png
:width: 70%
:align: center
```

Задатак: Написати програм којим се уноси n елемената целобројног низа,
а затим се врши инвертовање унетог низа на оба начина. Исписати инвертоване
низове.

Решење без увођења новог низа:

```c
#include <stdio.h> 
main() 
{ 
	int b,i,j,a[50],n;
	printf("Unesi koliko elemenata niza unosis ");
	scanf("%d",&n);
	printf ("Unesi %d elemenata niza: \n",n);
	for (i=0; i<n; i++)
	{ 
  		printf ("a[%d]=",i);
		scanf ("%d",&a[i]);
	}
	printf("\nUneti niz:\n"); 
	for(i=0;i<n;i++) 
	{ 
  		printf("a[%d]=%d\n",i,a[i]); 
	} 
	for (i=0, j=n-1; i<j; i++, j--) 
	{ 
    		b=a[i]; a[i]=a[j]; a[j]=b; 
	} 
	printf("\nInvertovani niz :\n");
	for(i=0;i<n;i++) 
	{ 
  		printf("a[%d]=%d\n",i,a[i]); 
	}
}
```

Решење са увођењем новог низа:

```c
#include <stdio.h> 
main() 
{ 
	int i,j,a[50],b[50],n;
	printf("Unesi koliko elemenata niza unosis ");
	scanf("%d",&n);
	printf ("Unesi %d elemenata niza: \n",n);
	for (i=0; i<n; i++)
	{ 
  		printf ("a[%d]=",i);
		scanf ("%d",&a[i]);
	}
	for(i=0; i<n; i++)
      		b[n-i]= a[i];
	printf("\nInvertovani niz :\n");
	for(i=0;i<n;i++) 
	{ 
  		printf("a[%d]=%d\n",i,a[i]); 
	}
}
```

Излаз:

```text
Unesi koliko elemenata niza unosis 5
Unesi 5 elemenata niza:
a[0]=1
a[1]=2
a[2]=3
a[3]=4
a[4]=5

Invertovani niz :
a[0]=5
a[1]=4
a[2]=3
a[3]=2
a[4]=1
```
