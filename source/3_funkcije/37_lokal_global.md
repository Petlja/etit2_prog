# Локалне и глобалне променљиве

Већ смо напоменули да су променљиве дефинисане на почетку тела функције локалне
и видљиве су само унутар функције. Њима се може приступити само унутар функције
и другим функцијама су оне невидљиве, недоступне.

Због ове особине могуће је употребити исто име за променљиве у више функција.
Наравно, увек задржавамо право да употребимо различита имена.

На пример, посматрајмо две функције:

```c
int zbir(int x, int y)
{
    int z = x + y;
    return z;
}

int razlika(int x, int y)
{
    int z = x - y;
    return z;
}
```

Параметар `z` у функцији `zbir` је потпуно независтан од параметра `z` у функцији
`razlika`. То су две сасвим различите променљиве. Ово правило важи и за главну
функцију у којој позивамо наше креиране функције.

```c
int main(void)
{
    int x, y, z;
    ...
    z = zbir(x, y);                            
    printf("Suma brojeva je: %d", z); 
    z = razlika(x, y);                        
    printf("Razlika brojeva je: %d", z);
    return 0;
}
```

Постоје променљиве (идентификатори) које су заједничке за већи број функција.
Такве променљиве се називају глобалне променљиве. Оне се дефинишу изван било
које функције. Видљиве су од тренутка декларисања до краја програма. Зато су
видљиве у свим функцијама и може им се приступити и мењати вредност из било
које функције.

Ово значи да се подаци из једне функције могу прослеђивати у другу функцију не
само посредством стварних параметара позивом функције, већ и преко глобалних
променљивих.

Међутим, при коришћењу глобалних променљивих морају се испоштовати следећа правила,
посебно око њиховог именовања:

- Морају бити декларисане пре функције,
- Не смеју имати исто име као функција,
- Сви аргументи функције морају имати другачије име од глобалне променљиве,
- Све локалне променљиве у функцији морају имати другачије име од глобалне променљиве.

Посматрајмо промену вредности глобалне променљиве s у следећем примеру:

```c
#include<stdio.h>
int s = 7;
void fun1()
{
    s++;
}

void fun2(int a)
{
    s = a - 5;
}
 
int main(void)
{
    fun1(); // s = 8
    s = s - 5; // s = 3
    printf("Vrednost promenljive s je %d\n", s);
    fun2(3); // s = -2
    printf("Vrednost promenljive s je %d\n", s);
    return 0;
}
```

Резултат извршавања програма:

```text
Vrednost promenljive s je 3
Vrednost promenljive s je -2
```

После позива функције `fun1()` вредност `s` се инкрементира и добија вредност `s = 8`.

Наредбом `s = s – 5` променљивој `s` се приступа из главне функције и она сада има
вредност `s = 3`.

Позивом функције `fun2(3)` прослеђује се вредност `а = 3`, па је `s = -2`.

Глобални подаци постоје за све време извршавања програма. Ако се не наведе почетна
вредност, подразумева се да је `0`.
