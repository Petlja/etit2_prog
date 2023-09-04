# Показивачи на функције

У ранијем излагању споменули смо да функције заузимају меморијски простор и да самим
тим имају своје адресе. Отуда је могуће дефинисати показиваче на функције.

Општи облик декларације показивача на функције је:

`тип (*име_показивача) (листа параметара)`

*Тип* представља тип резултата функције на који показивач показује.

*Листа параметара* одређује број и типове параметара функција на који показивач показује.

Наредбом…

```c
double (*pfun) (int, float);
```

…дефинише се показивач `pfun` на функције чија је вредност типа `double` и које имају два
параметра типа `int`, односно типа `float`.

```{infonote}
Два показивача су истог типа ако се сви ови елементи поклапају.
Показивач `double (*pfun1) (int, float)` је истог типа као `*pfun`.
Показивач `double (*pfun2) (float, int)` није истог типа као `*pfun`.
Показивач `int (*pfun2) (int, int)` није истог типа као `*pfun`.
```

Правила за показиваче на податке важе и за показиваче на функције. Показивачи на
функције могу да се додељују међусобно, али само ако су истог типа.

Као пример, посматрајмо познату функцију:

```c
int zbir(int a, int b)
{
    return a + b;
}
```

Показивач на ову функцију мора да има следећи облик:

```c
int (*pfun) (int, int);
```

Наредбом `pfun = zbir` показивачу додељујемо адресу функције `zbir`.

Вредности коју враћа функција приступа се са аргументима `a` и `b` `(*pfun)(a, b)`.
Ово је заправо као да смо позвали функцију zbir са параметрима `а` и `b`.

Изглед главног програма:

```c
main()
{
    int (*pfun)(int, int);
    pfun = zbir;
    printf("Zbir je %d\n", (*pfun)(10, 13));
}
```

Резултат извршавања програма:

```text
Zbir je: 23
```

Укључимо сада у причу и функцију `razlika`:

```c
int razlika(int a, int b)
{
    return a - b;
}
```

Изменимо главни програм:

```c
main()
{
    int (*pfun)(int, int);
    pfun = zbir;
    printf("Zbir je %d\n", (*pfun)(10, 13));
    pfun = razlika;
    printf("Razlika je %d", (*pfun)(10,13));
}
```

Резултат извршавања програма:

```text
Zbir je: 23
Razlika je -3
```
```{questionnote}
Шта смо урадили у програму?
```

Показивачу `pfun` доделили смо адресу функције `razlika`. Сада показивач показује
на функцију `razlika` и прослеђивањем аргумената узимамо вредност функције.

Да би креирали показивач истог типа за све четири основне математичке операције,
морамо да променимо елементе показивача, јер количник, сећаш се, враћа вредност
типа `double`.

```c
double (*pfun)( double, double);
```

```{questionnote}
Покушај да на основу и креираних функција `zbir`, `razlika`, `proizvod`, `kolicnik` и
дефинисаног показивача на функције одредиш вредности основних рачунских операција за
променљиве `a` и `b`.
```

```c
double zbir(double a, double b)
{
    return a + b;
}

double razlika(double a, double b)
{
    return a - b;
}
double proizvod(double a, double b)
{
    return a * b;
}


double kolicnik(double a, double b)
{
    return a / b;
}

int main(void)
{
    double a,b,(*pfun)(double, double);
    printf("Unesi a: ");
    scanf("%lf", &a);
    printf("Unesi b: ");
    scanf("%lf", &b);
    pfun = zbir;
    printf("\nZbir je %.2lf\n", (*pfun)(a, b));
    pfun = razlika;
    printf("Razlika je %.2lf\n", (*pfun)(a, b));
    pfun = proizvod;
    printf("Proizvod je %.2lf\n", (*pfun)(a, b));
    pfun = kolicnik;
    printf("Kolicnik je %.2lf\n", (*pfun)(a, b));
    pfun = pow;
    printf("Stepen je %.2lf", (*pfun)(a, b));
    return 0;
}
```

Резултат извршавања програма:

```text
Unesi a: 3
Unesi b: 4

Zbir je 7.00
Razlika je -1.00
Proizvod je 12.00
Kolicnik je 0.75
Stepen je 81.00
```

Обрати пажњу да смо у последњем кораку позвали математичку функцију `pow`. На то
имамо право, јер је њен општи облик, сећаш се, `pow(double, double)`, па је показивач
истог типа као показивач на нашу функцију.

И за крај, у главном програму креираћемо низ показивача.

```c
int main(void)
{
    double a, b, (*pfun)(double, double);
    int i;
    printf("Unesi a: ");
    scanf("%lf", &a);
    printf("Unesi b: ");
    scanf("%lf", &b);
    double (*funOperacije[5])(double, double) = {zbir, razlika, proizvod, kolicnik, pow};
    printf("\nZbir je %.2lf\n", funOperacije[0](a, b));
     printf("Razlika je %.2lf\n", funOperacije[1](a, b));
     printf("Proizvod je %.2lf\n", funOperacije[2](a, b));
     printf("Kolicnik je %.2lf\n", funOperacije[3](a, b));
     printf("Stepen je %.2lf ", funOperacije[4](a, b));
	 return 0;
}
```

Резултат извршавања програма:

```text
Unesi a: 3
Unesi b: 4

Zbir je 7.00
Razlika je -1.00
Proizvod je 12.00
Kolicnik je 0.75
Stepen je 81.00
```
