# Шта смо научили
## Реши квиз
### Библиотека <stdio.h>
Провери своје знање. Пробај да решиш квиз.
```{mchoice}
:answer1: scanf 
:answer2: printf
:answer3: putchar
:answer4: getchar
:correct: 1

Функција за форматирани унос знака је (са конверзијом):
```

```{mchoice}
:answer1: scanf 
:answer2: printf
:answer3: putchar
:answer4: getchar
:correct: 4

Функција за неформатирани унос знака (без конверзије) је:
```

```{mchoice}
:answer1: scanf 
:answer2: getchar
:answer3: putchar
:answer4: printf
:correct: 4

Функција за форматирани испис знака је (са конверзијом):
```

```{mchoice}
:answer1: scanf 
:answer2: printf
:answer3: putchar
:answer4: getchar
:correct: 3

Функција за неформатирани испис знака (без конверзије) је:
```

```{mchoice}
:answer1: puts, gets
:answer2: putchar, gets
:answer3: getchar, puts
:answer4: printf, scanf 
:correct: 1

Функције за неформатирани унос и испис стринга (без конверзије) су:
```

```{mchoice}
:answer1: puts, gets
:answer2: putchar, gets
:answer3: getchar, puts
:answer4: printf, scanf 
:correct: 4

Функције за форматирани унос и испис стринга (са конверзијом) су:
```


Дате су линије кода: 

```c
#include <stdio.h>
int main(void)
{
    char s[] = "Petrovic Pero";
    printf("Ime je %-10.3s", s);
    return 0;
}
```

```{questionnote}
Шта ће бити исписано на излазу?
```

**Одговор**:

`   Ime je      Per`

-10.3 резервише 10 места за испис стринга који почиње од леве ивице за 3 карактера.

### Библиотека <string.h>

Провери своје знање. Пробај да решиш квиз.

```{mchoice}
:answer1: Дописује низ s на крај низа t
:answer2: Преписује знаковни низ s у низ t укључујући и \0
:answer3: Преписује знаковни низ t у низ s укључујући и \0
:answer4: Дописује низ t на крај низа s
:correct: 2

Функција strcpy(t, s): 
```

```{mchoice}
:answer1: Дописује низ s на крај низа t
:answer2: Преписује знаковни низ s у низ t укључујући и \0
:answer3: Преписује знаковни низ t у низ s укључујући и \0
:answer4: Дописује низ t на крај низа s
:correct: 1

Функција strcat(t, s): 
```

```{questionnote}
Нa програмском језику С, декларисани су и иницијализовани стрингови:

```c
char s1[] = "crvena zvezda";
char s2[] = "zelengora";
```
Одредити садржај стрингова по извршењу следеће наредбе:

```c
strncpy(s1,s2,3);
```

**Решење**: 

```text
s1 = "zelena zvezda"
s2 =" zelengora"
```

```{questionnote}
Нa програмском језику С, декларисани су стрингови:

```c
char s1[100] = "", s2[100] = "biografija";
char *t = "planarna geometrija";
```
Са леве стране написани су изрази. Одредити вредност стринга по извршењу наведене наредбе (наредбе не посматрати као секвенцу, већ независно једну од друге):
```text
strcpy(s1, t);                      s1 = "planarna geometrija"
strncpy(s1, t, 4);                  s1 = "plan"
strcpy(s2, t);                      s2 = "planarna geometrija"
strncpy(s2, t + 9, 3);              s2 = "geografija"
```
### Библиотека <stdlib.h>
Провери своје знање. Пробај да решиш квиз.
```{questionnote}
Дата је линија кода: 

```c
#include<stdio.h>
int main(void)
{
    char a[] = "k234";
    int b = 5, c;
    printf("c = %d",atoi(a) + b);
    return 0;
}
```

```{mchoice}
:answer1: c = 0
:answer2: c = 5
:answer3: c = 238
:correct: 2

Шта се исписује на излазу?
```
### Пробај да одговориш на следећа питања

```{questionnote}
Дат је прототип функције написан у програмском језику С:\
`void test(char *a, char k);`\
У main функцији дате су следеће декларације променљивих:\
`char s1[20], *s2, s3;`
```
```{mchoice}
:answer1: test (s2, s1[i]);
:answer2: (s2, s1);
:answer3: (s2, ‘A’);
:answer4: (s1, s3);
:answer5: (*s2, s3);
:answer6: (s3, &s1);
:correct: 1,3,4

Одредити који су исправно написани позиви декларисане функције
```
```{questionnote}
Дат је прототип функције написан у програмском језику С:\
`void test(char *a, char k);`\
У main функцији дате су следеће декларације променљивих:\
`char s1[20], *s2, s3;`
```
```{mchoice}
:answer1: test (s2, s1[i]);
:answer2: (s2, s1);
:answer3: (s2, ‘A’);
:answer4: (s1, s3);
:answer5: (*s2, s3);
:answer6: (s3, &s1);
:correct: 1,3,4

Одредити који су исправно написани позиви декларисане функције
```

```{questionnote}
Дат је кôд функције **funkcija** написане у програмском језику C 
```
```c
int funkcija(char c)
{
    return ((c>='a'&&c<='z') || (c>='A'&&c<='Z') || (c>='0'&&c<='9')) ? 1 : 0;
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
    while(*s==' ' || *s=='\t') 
    s++;
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
    while((c=getchar())!='\n')
        *temp++=c;
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
На Петљи можете решавати задатке из Методичке збирке задатака из основа програмирања, део „Карактери и ниске“ који се налазе на линку
[Metodicka zbirka zadataka](https://petlja.org/biblioteka/r/Zbirka/04%20Nizovi/02%20niske)
кристећи он лајн С или С/С++ компајлер. За почетак пробајте да решите задатак
из збирке који се налази на линку
[Prezime pa ime](https://petlja.org/biblioteka/r/Zbirka/prezime_pa_ime).