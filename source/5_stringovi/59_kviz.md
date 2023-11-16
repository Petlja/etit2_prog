# Шта смо научили
## Реши квиз
```{mchoice}
:answer1: test (s2, s1[i]);
:answer2: (s2, s1);
:answer3: (s2, ‘A’);
:answer4: (s1, s3);
:answer5: (*s2, s3);
:answer6: (s3, &s1);
:correct: 1,3,4

Дат је прототип функције написан у програмском језику С:
`void test(char *a, char k);`
У main функцији дате су следеће декларације променљивих:
`char s1[20], *s2, s3;`
Одредити који су исправно написани позиви декларисане функције
```
**Образложење**
Исправно су написани позиви функција под 1, 3 и 4 јер је први параметар у функцији показивач, а други карактер. 

У одговору под 2 test (s2, s1);  s1 је низ а не карактер. 

У одговору под 5 test (*s2, s3); s2 је показивач на показивач.

У одговору под 6 test (s3, &s1); s3 није низ, а s1 је адреса а не карактер.

```{questionnote}
Дат је програм написан у програмском језику С. 
```
```c
#include<stdio.h>
int main(void)
{
    char izbor;
    printf("Za izbor unesite D ili N: ");
    do
    {
        izbor = getchar();
    }
    while(izbor!= 'D'&& izbor!='N');
    putchar(izbor);
    return(0);
}
```
```{mchoice}
:answer1: На екрану се приказује унето слово d, излази се из петље и наставља са извршењем програма
:answer2: На екрану се приказује унето слово d, али се не излази из петље већ се чека унос слова D или N
:answer3: На екрану се не приказује ништа и програм се понаша као да „не реагује“ на унос слова d
:answer4: На екрану се не приказује унето слово, већ само порука којом се тражи поновни унос
:correct: 3

Одредити шта ће се исписати на екрану након уноса слова d са конзоле
```
```{questionnote}
Дат је кôд функције **funkcija** написане у програмском језику C 
```
```c
int funkcija(char c)
{
return ((c>='a'&&c<='z') ||
(c>='A'&&c<='Z') ||
(c>='0'&&c<='9')) ? 1 : 0;
}
```
```{mchoice}
:answer1: isupper
:answer2: isalpha
:answer3: isalnum
:answer4: strchr
:answer5: atoi
:answer6: gets
:correct: 3

Изабрати којој функцији из стандардне библиотеке функција **ctype.h** одговара дата функција
```
```{questionnote}
Дат је кôд функције **funkcija** написане у програмском језику C 
```
```c
int funkcija() (char c)
{
return (c>='A'&& c<='Z') ? 1 : 0;
}
```
```{mchoice}
:answer1: isupper
:answer2: isalpha
:answer3: isalnum
:answer4: strchr
:answer5: atoi
:answer6: strcmp
:correct: 1

Изабрати којој функцији из стандардне библиотеке функција **ctype.h** одговара дата функција
```
```{questionnote}
Дат је кôд функције **funkcija** написане у програмском језику C 
```
```c
int funkcija(char *s) 
{
    int n, sign;
    while(*s==' ' || *s=='\t') s++;
    sign = (*s=='-') ? -1 : 1;
    if(*s=='+' || *s=='-') s++;
    for(n=0; *s>='0'&& *s<='9'; s++) n=10*n+ *s - '0';
    return (!*s) ? sign*n : 0;
}

```
```{mchoice}
:answer1: isupper
:answer2: isalpha
:answer3: strcmp
:answer4: strchr
:answer5: atoi
:answer6: gets
:correct: 5

Изабрати којој функцији из стандардне библиотеке одговара дата функција
```
```{questionnote}
Дат је кôд функције **funkcija** написане у програмском језику C 
```
```c
char * funkcija(char *s) 
{
    char c,*temp;
    temp=s;
    while((c=getchar())!='\n')*temp++=c;
    *temp='\0';
    return s;
}

```
```{mchoice}
:answer1: isupper
:answer2: isalpha
:answer3: isalnum
:answer4: strchr
:answer5: atoi
:answer6: gets
:correct: 6

Изабрати којој функцији из стандардне библиотеке одговара дата функција
```
```{questionnote}
Дат је кôд функције **funkcija** написане у програмском језику C 
```
```c
int funkcija(char *s, char *t) 
{
    char tempt, temps;
    while(*s && *t)
    {
        if(*t>='A'&& *t<='Z') 
            tempt = 'a' + *t -'A';
        else 
            tempt=*t;
        if(*s>='A'&& *s<='Z') 
            temps = 'a' + *s -'A';
        else 
            temps=*s;
        if(temps != tempt) 
            return temps - tempt;
        else s++, t++;
    }
    return *s - *t; .
}

```
```{mchoice}
:answer1: isupper
:answer2: isalpha
:answer3: isalnum
:answer4: strchr
:answer5: strcmp
:answer6: gets
:correct: 5

Изабрати којој функцији из стандардне библиотеке одговара дата функција
```
```{questionnote}
На програмском језику C декларисани су стрингови:

```

```c
char s1[100]="", s2[100]="geografija";
char *t="nacrtna geometrija";
```
```{mchoice}
:answer1: nacrtna geometrija
:answer2: nacr
:answer3: nacrtna
:answer4: eomgrafija
:correct: 1

Одредити вредност стринга `s1` по извршењу наведене наредбе `strcpy(s1, t);` 

```
```{questionnote}
На програмском језику C декларисани су стрингови:

```
```c
char s1[100]="", s2[100]="geografija";
char *t="nacrtna geometrija";
```

```{mchoice}
:answer1: geometrija
:answer2: eomgrafija
:answer3: nacrtna geometrija
:answer4: nacr
:correct: 4

Одредити вредност стринга `s1` по извршењу наведене наредбе `strncpy(s1, t, 4); 
```
```{questionnote}
На програмском језику C декларисани су стрингови:

```
```c
char s1[100]="", s2[100]="geografija";
char *t="nacrtna geometrija";
```
```{mchoice}
:answer1: nacrtna geometrija
:answer2: eomgrafija
:answer3: nacrtnageometrija
:answer4: nacr
:correct: 1

Одредити вредност стринга `s2` по извршењу наведене наредбе `strcpy(s2, t);` 
```
```{questionnote}
На програмском језику C декларисани су стрингови:

```
```c
char s1[100]="", s2[100]="geografija";
char *t="nacrtna geometrija";
```
```{mchoice}
:answer1: nacrtna geometrija
:answer2: eomgrafija
:answer3: grafija
:answer4: nacr
:correct: 1

Одредити вредност стринга `s2` по извршењу наведене наредбе `strncpy(s2,t+9,3);` 
```
```{questionnote}
У програмском језику C дат је кôд  
```
```c
#include<stdio.h>
#include <string.h>
int main(void)
{
char s1[]="Kratka Servisna Poruka", *s2, *s3;
s2=strchr(s1,'S');
s3=strrchr(s2,'P');
strncpy(s1+1,s2,1);
strcpy(s1+2,s3);
puts(s1);
puts(s2);
puts(s3);
return(0);
}

```
```{mchoice}
:answer1: Poruka
:answer2: KSP
:answer3: KSPoruka
:answer4: SerPoruka
:answer5: а
:correct: 3

Одредити вредност стринга `s1` по извршењу програма 
```
```{questionnote}
У програмском језику C дат је кôд  
```
```c
#include<stdio.h>
#include <string.h>
int main(void)
{
char s1[]="Kratka Servisna Poruka", *s2, *s3;
s2=strchr(s1,'S');
s3=strrchr(s2,'P');
strncpy(s1+1,s2,1);
strcpy(s1+2,s3);
puts(s1);
puts(s2);
puts(s3);
return(0);
}

```
```{mchoice}
:answer1: Poruka
:answer2: KSP
:answer3: KSPoruka
:answer4: SerPoruka
:answer5: а
:correct: 5

Одредити вредност стринга `s2` по извршењу програма 
```
```{questionnote}
У програмском језику C дат је кôд  
```
```c
#include<stdio.h>
#include <string.h>
int main(void)
{
char s1[]="Kratka Servisna Poruka", *s2, *s3;
s2=strchr(s1,'S');
s3=strrchr(s2,'P');
strncpy(s1+1,s2,1);
strcpy(s1+2,s3);
puts(s1);
puts(s2);
puts(s3);
return(0);
}

```
```{mchoice}
:answer1: Poruka
:answer2: KSP
:answer3: KSPoruka
:answer4: SerPoruka
:answer5: а
:correct: 1

Одредити вредност стринга `s3` по извршењу програма 
```
На Петљи можете решавати задатке из Методичке збирке задатака из основа програмирања, део „Матрице“ који се налазе на линку
[Metodicka zbirka zadataka](https://petlja.org/biblioteka/r/Zbirka/04%20Nizovi/02%20niske)
кристећи он лајн С или С/С++ компајлер. За почетак пробајте да решите задатак
из збирке који се налази на линку
[Prezime pa ime](https://petlja.org/biblioteka/r/Zbirka/prezime_pa_ime).