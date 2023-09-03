# Функције које враћају показиваче

Показивачи, за разлику од низова, могу да буду вредност функције. Tо је зато што
показивачи спадају у тзв. појединачне податке. Сети се приче о показивачимa – они
показују на појединачне податке, а ако показују на низ, садрже адресу само првог
елемента. То се поклапа са оном причом да функције враћају само једну вредност.

Ако је вредност функције показивач, у заглавље у део за тип вредности додаје се `*`.

Пример 1:

Креирај функцију за одређивање највећег од три унета броја. Функција као вредност
враћа показивач.

```c
#include<stdio.h>
int* pmax(int a, int b, int c)
{
	int* max;
	max = &a;
	if (b > *max)
		*max = b;
	if (c > *max)
		*max = c;
	return max;
 
}
```

Наредбом `return max` у главни програм враћа се адреса највећег од три броја који су као
аргументи прослеђени у функцију.

Приликом позива функције, `pmax(a, b, c)` је показивач, а вредност добијамо са `*pmax(a, b, c)`.

```c
main()
{
	int max;
	int a = 7, b = 3, c = 9;
	max = *pmax(a, b, c);
	printf("Najveci od brojeva je %d", max);
}
```

Резултат извршавања програма:

```text
Najveci od brojeva je 9
```

Пример 2:

Креирај функцију за одређивање суме елемената низа. Функција као вредност враћа
показивач.

```c
#include<stdio.h>
int* pSuma(int a[], int n)
{
	int s = 0;
	int* ps, * p;
	ps = &s;
	for (p = a;p < a + n;p++)
		s = *p + s;
	return ps;
}
main()
{
	int a[7] = { 5,8,3,11,45,33,19 };
	int* ps, s;
	ps = pSuma(a, 7);
	printf("Suma elemenata nizaje: %d\n", *ps);
	s = *pSuma(a, 7);
	printf("Suma elemenata nizaje: %d\n", s);
}
```

Резултат извршавања програма:

```text
Suma elemenata nizaje: 124
Suma elemenata nizaje: 124
```

Вежбање

Креирај функцију за одређивање највећег елемента низа. Функција као вредност враћа показивач.

```c
#include<stdio.h>
int* pmax(int a[], int n)
{
	int* pm, * p;
	pm = a;
	for (p = a + 1;p < a + n;p++)
		if (*p > *pm) pm = p;
	return pm;
}
main()
{
	int a[7] = { 5,8,3,11,45,33,19 };
	int* pm, max;
	pm = pmax(a, 7);
	printf("Maksimalni element niza je: %d\n", *pm);
	max = *pmax(a, 7);
	printf("Maksimalni element niza je: %d\n", max);
}
```

Резултат извршавања програма:

```text
Maksimalni element niza je: 45
Maksimalni element niza je: 45
```
