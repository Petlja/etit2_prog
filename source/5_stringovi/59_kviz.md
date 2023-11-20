# Шта смо научили
## Реши квиз
### Библиотека <stdio.h>
Провери своје знање. Пробај да решиш квиз.\
**Питање 1:**
```{mchoice}
:answer1: scanf 
:answer2: printf
:answer3: putchar
:answer4: getchar
:correct: 1

Функција за форматирани унос знака је (са конверзијом):
```
**Питање 2:**
```{mchoice}
:answer1: scanf 
:answer2: printf
:answer3: putchar
:answer4: getchar
:correct: 4

Функција за неформатирани унос знака (без конверзије) је:
```
**Питање 3:**
```{mchoice}
:answer1: scanf 
:answer2: getchar
:answer3: putchar
:answer4: printf
:correct: 4

Функција за форматирани испис знака је (са конверзијом):
```
**Питање 4:**
```{mchoice}
:answer1: scanf 
:answer2: printf
:answer3: putchar
:answer4: getchar
:correct: 3

Функција за неформатирани испис знака (без конверзије) је:
```
**Питање 5:**
```{mchoice}
:answer1: puts, gets
:answer2: putchar, gets
:answer3: getchar, puts
:answer4: printf, scanf 
:correct: 1

Функције за неформатирани унос и испис стринга (без конверзије) су:
```
**Питање 6:**
```{mchoice}
:answer1: puts, gets
:answer2: putchar, gets
:answer3: getchar, puts
:answer4: printf, scanf 
:correct: 4
Функције за форматирани унос и испис стринга (са конверзијом) су:
```
**Питање 7:**
Дате су линије кода:

```c
#include <stdio.h>
int main(void)
{
    char s[] = "Petrovic Pero";
    printf("(Ime je %-10.3s)", s);
    return 0;
}
```
```{mchoice}
:answer1: (`Ime je       Per`)
:answer2: (`Ime je         Pero`)
:answer3: (`Ime je Petrovic Per`)
:correct: 1
Шта ће бити исписано на излазу?
```

### Библиотека <string.h>

**Питање 8:**

```{mchoice}
:answer1: Дописује низ s на крај низа t
:answer2: Преписује знаковни низ s у низ t укључујући и \0
:answer3: Преписује знаковни низ t у низ s укључујући и \0
:answer4: Дописује низ t на крај низа s
:correct: 2

Функција strcpy(t, s): 
```
**Питање 9:**
```{mchoice}
:answer1: Дописује низ s на крај низа t
:answer2: Преписује знаковни низ s у низ t укључујући и \0
:answer3: Преписује знаковни низ t у низ s укључујући и \0
:answer4: Дописује низ t на крај низа s
:correct: 1

Функција strcat(t, s): 
```
### Библиотека <stdlib.h>
**Питање 10:**
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
### Библиотека <ctype.h>
**Питање 11:**
```{mchoice}
:answer1: stdio.h
:answer2: ctype.h
:answer3: string.h
:answer4: stdlib.h
:correct: 2
Библиотечке функције за рад са знаковима налазе се у библиотеци:
Изаберите исправан одговор.
```
### Пробај да одговориш на следећа питања

**Питање 12:**
Дат је прототип функције написан у програмском језику С:\
`void test(char *a, char k);`\
У main функцији дате су следеће декларације променљивих:\
`char s1[20], *s2, s3;`
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
**Питање 13:**
Дат је прототип функције написан у програмском језику С:\
`void test(char *a, char k);`\
У main функцији дате су следеће декларације променљивих:\
`char s1[20], *s2, s3;`
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
**Питање 14:**
Дат је кôд функције **funkcija** написане у програмском језику C 
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
**Питање 15:**
Дат је кôд функције **funkcija** написане у програмском језику C 

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

Изабрати којој функцији из стандардне библиотеке функција ctype.h\ одговара дата функција
```
**Питање 16:**
Дат је кôд функције **funkcija** написане у програмском језику C 
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
**Питање 17:**
Дат је кôд функције **funkcija** написане у програмском језику C 
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
**Питање 18:**
Дат је кôд функције **funkcija** написане у програмском језику C 

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
**Питање 19:**
На програмском језику C декларисани су стрингови:

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
Одредити вредност стринга s1 по извршењу наведене наредбе strcpy(s1, t);
```
**Питање 20:**
На програмском језику C декларисани су стрингови:
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
**Питање 21:**
На програмском језику C декларисани су стрингови:

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
**Питање 22:**
На програмском језику C декларисани су стрингови:
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
**Питање 23:**
У програмском језику C дат је кôд :
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
**Питање 24:**
У програмском језику C дат је кôд:
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

Одредити вредност стринга s2 по извршењу програма 
```
**Питање 25:**
У програмском језику C дат је кôд: 
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
### Пробајте да напишете следеће програме:
```{questionnote}
Написати програм који броји децималне цифре у улазном тексту до ознаке за крај уноса `ЕОF`. Написати програм без коришћења функција за проверу карактера, а затим користећи функцију `isdigit`.
```
**Решење 1:**
```c
#include <stdio.h>
int main(void)
{
    int c, n=0;
    printf("Unesi tekst pa enter i ctrl+z na kraju\n" );
    while((c=getchar()) != EOF)
        if(c>='0'&& c<='9') 
            n++;
    printf("\n Broj cifara: %d.\n", n); 
return(0);
}

```
**Решење 2:**
```c
#include <stdio.h>
int main(void)
{
    int c, n=0;
    printf("Unesi tekst pa enter i ctrl+z na kraju\n" );
    while((c=getchar()) != EOF)
        if(isdigit(c)) n++;
            printf("\n Broj cifara: %d.\n",n); 
return(0);
}

```
Излаз:
```text
Unesi tekst pa enter i ctrl+z na kraju
Ovaj red 123 mora da ima 4 cifre i zavrsen je sa ctrl+z
^Z 
Broj cifara: 4.
```
```{questionnote}
Написати програм за одређивање броја великих слова, малих слова и цифара у улазном тексту. Унос текста се завршава сигналом ЕОF. Написати програм без коришћења функција за проверу карактера, а затим користећи функцију `isdigit`.
```
**Решење 1:**
```c
#include <stdio.h>
int main(void)
{
    int c, veliko=0, malo=0, cifra=0;
    while((c = getchar()) != EOF)
    {
        if(c >= 'A' && c <= 'Z')
            veliko++; 
        if(c >= 'a' && c <= 'z')	
            malo++; 
        if(c >= '0' && c <= '9')	
            cifra++;
    }
    printf(" Velika: %d\n", veliko); 
    printf(" Mala:	%d\n", malo); 
    printf(" Cifre:	%d\n",cifra); 
    return(0);
}

```
**Решење 2:**
```c
#include <stdio.h>
int main(void)
{
    int c, veliko=0, malo=0, cifra=0;
    while((c = getchar()) != EOF)
    {
        veliko = veliko+(isupper(c) != 0);
        malo = malo+(islower(c) != 0);
        cifra =cifra+(isdigit(c) != 0);
    }
    printf(" Velika: %d\n", veliko);
    printf(" Mala:	%d\n", malo); 
    printf(" Cifre:	%d\n", cifra);
    return(0);
}

```
Излаз:
```text
Ovaj red sadrzi VELIKA mala slova i cifre 123 i zavrsava se sa ctrl+Z
^Z
Velika: 9
Mala: 43
Cifre: 3 
```
```{questionnote}
Написати програм за одређивање броја појављивања слова А у улазном тексту и изразити ту вредност процентуално у односу на све унете знаке. Унос текста се завршава сигналом `ЕОF`.
```
**Решење:**
```c
#include <stdio.h>
int main(void)
{
    int c, n=0, u=0;
    float p;
    while((c = getchar()) != EOF)
    {
        u++;
        if(c=='A')
            n++;
    }
    p=(float)n/u*100;
    printf("\nUkupno znakova: %d", u); 
    printf("\nUkupno slovo A: %d", n); 
    printf("\nU procentima: %.2f%\n", p);
    return(0);
}

```
Излаз:
```text
Ovde ima dva velika slova AA
^Z

Ukupno znakova: 29
Ukupno slovo A: 2
U procentima: 6.90
```
### Домаћи задатак
Пробајте за домаћи да решите следеће задатке. Решења задатака можете проверити на дну ове странице.
```{questionnote}
Домаћи 1. Написати програм који броји празне знакове (размак, хоризонтални табулатор и нови ред), слова, децималне цифре, као и све знакове улазног текста до ознаке за крај уноса `ЕОF`. Програм написати без коришћења библиотечких функција, а затим са коришћењем библиотечких функција.
```
```{questionnote}
Домаћи 2. Написати програм за одређивање броја самогласника и сугласника у улазном тексту. Унос текста се завршава сигналом `ЕОF`.
```
```{questionnote}
Домаћи 3. Написати програм који броји карактере улазног текста до прве децималне цифре. Унос текста се завршава сигналом `EOF`.
```
```{questionnote}
Домаћи 4.Написати програм који врши конверзију унетих великих слова у мала. Унос текста се завршава сигналом `EOF`.
```
```{questionnote}
Домаћи 5. Написати програм за проналажење најдужег учитаног реда текста. Унос редова се прекида кад се *** учита из реда.
```

### Решења домаћих задатака

**Домаћи 1 Решење 1:**
```c
#include <stdio.h>
int main(void)
{
    int c, nk=0, nr=0, nb=0, ns=0;
    while((c=getchar()) != EOF)
    {
        if((c==' ') || (c=='\t') || (c=='\n'))	
            nr++;
        if(c>='0' && c<='9')	
            nb++;
        if((c>='a' && c<='z') || (c>='A' && c<='Z'))	
            ns++; 
        nk++;
    }
     printf("Razmaci: %d\n", nr); 
    printf("Cifre: %d\n", nb); 
    printf("Slova: %d\n", ns); 
    printf("Ukupno: %d\n",nk);
    return(0);
}

```
**Домаћи 1 Решење 2:**
```c
#include <stdio.h>
int main(void)
{
    int c, nk=0, nr=0, nb=0, ns=0;
    while((c=getchar()) != EOF)
    {
        if(isspace(c)) 
            nr++; 
        if(isdigit(c)) 
            nb++; 
        if(isalpha(c)) 
            ns++; 
        nk++;
    }
	printf(" Razmaci: %d\n", nr); 
	printf(" Cifre: %d\n", nb); 
	printf(" Slova: %d\n", ns); 
	printf(" Ukupno: %d\n",nk);
    return(0);
}

```
Излаз:
```text
Broj 1 i        broj 158
^Z
Razmaci: 12
Cifre: 4
Slova: 9
Ukupno: 25 
```
**Домаћи 2 Решење :**
```c
#include <stdio.h>
int main(void)
{
    int c, sugl=0, samog=0;
    while((c=getchar()) != EOF)
    {
        if((c>='a' && c<='z') || (c>='A' && c<='Z'))
        if(c=='a' || c=='e' || c=='i' || c=='o' || c=='u'|| c=='A' || c=='E' || c=='I' || c=='O' || c=='U') 
            samog++;
        else
            sugl++;;
    }
    printf("Samoglasnika: %d\n", samog); 
    printf("Suglasnika: %d\n", sugl); 
    return(0);
}
```
Излаз:
```text
Programski jezik C
^Z
Samoglasnika: 5
Suglasnika: 11
```
**Домаћи 3 Решење :**
```c
#include <stdio.h>
int main(void)
{
    int c, n=0;
    while((c=getchar()) != EOF)
    {
        if(isdigit(c)) 
        break; 
        n++;
    }
    printf("Broj znakova: %d\n", n); 
    return(0);
}
```
Излаз:
```text
Do broja 1 ce prebrojati broj karaktera
Broj znakova: 9
```
**Домаћи 4 Решење 1:**
```c
#include <stdio.h>
int main(void)
{
    int c;
    while((c=getchar()) != EOF)
    {
        if(c >= 'A' && c <= 'Z')
        c = c -'A' + 'a';
        putchar(c);
    }
    return(0);
}
```
**Домаћи 4 Решење 2:**
```c
#include <stdio.h>
int main(void)
{
    int c;
    while((c=getchar()) != EOF) 
        putchar(tolower(c));
    return(0);
}
```
Излаз:
```text
ovaj program PrEtVaRa sva VELIKA SLOVA u mala
ovaj program pretvara sva velika slova u mala
```
**Домаћи 5 Решење :**
```c
#include <stdio.h>
int main(void)
{
    char red[100], max[100]="";
    while (1)
    {
        gets (red);
        if (strcmp(red, "***")==0) 
        break;
        if (strlen(red)> 
        strlen(max)) 
        strcpy (max,red);
    }
    puts(max);
    return(0);
}
```
Излаз:
```text
Pronalazi najduzi ucitan red
I prekida se kada se ucita u novom redu
***
I prekida se kada se ucita u novom redu
```

На Петљи можете решавати задатке из Методичке збирке задатака из основа програмирања, део „Карактери и ниске“ који се налазе на линку
[Metodicka zbirka zadataka](https://petlja.org/biblioteka/r/Zbirka/04%20Nizovi/02%20niske)
кристећи он лајн С или С/С++ компајлер. За почетак пробајте да решите задатак
из збирке који се налази на линку
[Prezime pa ime](https://petlja.org/biblioteka/r/Zbirka/prezime_pa_ime).