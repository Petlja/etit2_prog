# Стрингови и показивачи

Рекли смо да је стринг низ карактера који на крају има `null` карактер.
Као што смо видели, постоје функције које одређују позицију карактера у стрингу користећи показиваче. То значи да се може приступити делу стринга или карактеру користећи показиваче. Померањем за 1 показивач се помера за 1 бајт, с обзиром да тип `char` заузима управо толико меморијског простора.

Значи, ако напишемо… 

```c
char *p;
char ime[] = "Pero";
ime = p;
```

… показивач `p` у овом случају показује на први елеменат низа знакова ime, односно у њему је записана адреса првог елемента `ime[0]`. Због тога се у позивима функција уместо `char ime[]` може писати char `*p`. Урадимо неколико примера.

```{questionnote}
Написати програм за унос и испис имена и презимена особе користећи показиваче.
```

```c
#include <stdio.h>
int main(void)
{
    char *s,ime[20];
    s = ime;
    printf("Unesi ime i prezime osobe: "); 
    gets(s);
    printf("Uneli ste %s",s);
    return 0;
}
```

Излаз:

```text
Unesi ime i prezime osobe: Petar Petrovic
Uneli ste Petar Petrovic
```

Примећујете да опет мора да се резервише број места за стринг. Ово у ствари значи да, када пишете функцију, низ без проблема можете да пренесете преко показивача у функцију.

```{questionnote}
Напишите функцију која рачуна дужину стринга. У функцију се као параметар уноси стринг преко показивача, а као резултат она враћа дужину.
```

```c
#include <stdio.h>
int duzina(char *s)
{
    int i;
    for (i = 0; s[i] != '\0'; i++ );
        return i;
}

int main(void)
{
    char *s, ime[20];
    s = ime;
    printf("Unesi ime i prezime osobe: "); 
    gets(s);
    printf("Uneli ste %s duzine %d", s, duzina(s));
}
```

Излаз:

```text
Unesi ime i prezime osobe: Petar Petrovic
Uneli ste Petar Petrovic duzine 14
```

```{questionnote}

Напишимо ову функцију мало другачије. У претходном примеру смо користили приступ елементу стринга `s[i]`. Овде ћемо за приступ елементима и бројање користити показивач `s`.
```

```c
#include <stdio.h>
int duzina1(char *s )
    {
    int i = 0;
    while(*s++ != '\0') 
        i++;
    return i;
}	

int main(void)
{
    char *s, ime[20];
    s = ime;
    printf("Unesi ime i prezime osobe: "); 
    gets(s);
    printf("Uneli ste %s duzine %d", s, duzina1(s));
}
```

Излаз: 

```text
Unesi ime i prezime osobe: Pero Petrovic
Uneli ste Pero Petrovic duzine 13
```

Знамо да су оператори `*` и `++` истог приоритета, и да је асоцијативност ове групе оператора са десна на лево. Ако узмемо у обзир оператор `++` иза показивачке промењиве значи да ће оператор `*` бити примењен на стару адресу показивача `s`. Тек након тога ће се показивач померити за један бајт и приступити наредном елементу. Показивач се помера све док не стигне до '\0' односно завршног `null` карактера.

```{questionnote}
Напишите функцију која проналази позицију првог појављивања карактера у стрингу. У функцију се као параметар уносе стринг преко показивача и карактер који се тражи, а као резултат враћа се показивач на позицију где је пронађен карактер. У супротном, функција треба да врати `NULL`. 
```

```c
#include <stdio.h>
char* nadji_prvi(char* s, char c)
{
    while (*s && *s != c)
        s++;
    if (*s)
        return s;
    else
        return NULL;
}

int main(void)
{
    char str[20], c;
    printf("Unesi string: ");
    gets(str);
    printf("Unesi trazeni karakter: ");
    c = getchar();
    if (nadji_prvi(str, c) != NULL)
        printf("\nNadjen je karakter na poziciji %d", (nadji_prvi(str, c) - str + 1));
    else
        printf("\nNije nadjen je karakter na poziciji ");
    return 0;
}
```

Излаз 1:

```text
Unesi string: Petrovic Petar
Unesi trazeni karakter: o

Nadjen je karakter na poziciji 5
```

Излаз 2:

```text
Unesi string: Petrovic Petar
Unesi trazeni karakter: M

Nije nadjen karakter na poziciji
```

```{questionnote}
Шта примећујеш у овом примеру?
```

Повратна вредност функције је показивач на позицију првог појављивања траженог карактера – у супротном она враћа `NULL`.

```{questionnote}
Напишите функцију која проналази и брише карактер у стрингу. У функцију се као параметар уносе стринг преко показивача и карактер који се брише, а као резултат функција нема повратну вредност. 
```

```c
#include<stdio.h>
void brisi_znak(char *s, char c)
{
    char *p = s;
    while(*p)
    {
        if(*p != c)
            *s++ = *p; 
        p++;
    }
    * s= '\0';
}

int main(void)
{
char str[20], c;
    printf("Unesi string: ");
    gets(str);
    printf("Unesi karakter koji brises: ");
    c = getchar();
    brisi_znak(str, c);
    printf("\nNakon brisanja string je: %s", str);
    return 0;
}
```

Излаз:

```text
Unesi string: Iz ovog stringa obrisacemo karakter a
Unesi karakter koji brises: a

Nakon brisanja string je: Iz ovog string obriscemo krter
```



Провери своје знање: Реши квиз.

<!---  Pitanja i odgovori treba da se preformulišu...
Дат је прототип функције написан у програмском језику С:

```c
void test(char *a, char k);
```

У `main` функцији дате су следеће декларације променљивих:

```c
char s1[20], *s2, s3;
```

```{mchoice}
:answer1: test(s2, s1[i]);
:answer2: test(s2, s1);
:answer3: test(s2, 'A');
:answer4: test(s1, s3);
:answer5: test(*s2, s3);
:correct: 1,3,4

Одредити који су исправно написани позиви декларисане функције:
```

Дат је програм написан у програмском језику С. 

```c
#include<stdio.h>
int main(void)
{
    char s[20] = {'A', 'c', 'a', ' ', 'j' ,'e' ,'\0' ,'d' ,'o' ,'b' ,'a' ,'r'};
	char t[12] = {'A' ,'c' ,'a' ,' ' ,'j' ,'e' ,'\0' ,'d' ,'o' ,'b' ,'a' ,'r'};
	char *poc = s + 7;
	printf("\nString = %s\n", poc);
	printf("String = %s\n", s + 4);
	printf("Znak = %c\n", *poc);
} 
```


```{mchoice}
:answer1: String = Aca je dobar, String = Aca, Znak = A
:answer2: String = dobar, String = je, Znak = d
:answer3: String = Acа, String = je, Znak = d
:answer4: String = dobar, String = dobar, Znak = d
:correct: 2

Одредити шта ће се исписати на екрану након његовог извршавања.
```


Дат је програм написан у програмском језику С. 

```c
#include<stdio.h>
main()
{
	char izbor;
	printf("Za izbor unesite D ili N: ");
	do
	{
	izbor = getchar();
	} while(izbor!= 'D'&& izbor!='N');
	putchar(izbor);
}
```

```{mchoice}
:answer1: На екрану се приказује унето слово d, излази се из петље и наставља са извршењем
програма.
:answer2: На екрану се приказује унето слово d, али се не излази из петље већ се чека унос
слова D или N.
:answer3: На екрану се не приказује ништа и програм се понаша као да „не реагује“ на унос
слова d.
:answer4: На екрану се не приказује унето слово, већ само порука којом се тражи поновни унос.
:correct: 3

Одредити шта ће се исписати на екрану након његовог извршавања.
```




Питање: Дат је кôд функције funkcija() написане у програмском језику C. Изабрати којој функцији из стандардне библиотеке функција ctype.h одговара дата функција.

int funkcija(char c)
{
return ((c>='a'&&c<='z') ||
(c>='A'&&c<='Z') ||
(c>='0'&&c<='9')) ? 1 : 0;
}

1. isupper
2. isalpha
3. gets
4. strncat
5. atoi
6. strchr
7. stricmp
8. isalnum

Одговор: Тачан одговор је под 8, isalnum.

Питање: Дат је кôд функције funkcija() написане у програмском језику C. Изабрати којој функцији из стандардне библиотеке функција ctype.h одговара дата функција.

int funkcija() (char c)
{
return (c>='A'&& c<='Z') ? 1 : 0;
}

1. isupper
2. isalpha
3. gets
4. strncat
5. atoi
6. strchr
7. strcmp

Одговор: Тачан одговор је под 1, isupper.

Питање: Дат је кôд функције funkcija() написане у програмском језику C. Изабрати којој стандардној функцији одговара дата функција.

int funkcija(char *s) 
{
int n, sign;
while(*s==' ' || *s=='\t') s++;
sign = (*s=='-') ? -1 : 1;
if(*s=='+' || *s=='-') s++;
for(n=0; *s>='0'&& *s<='9'; s++) n=10*n+ *s - '0';
return (!*s) ? sign*n : 0;
}

1. isupper
2. isalpha
3. gets
4. strncat
5. atoi
6. strchr
7. strcmp
Одговор: Тачан одговор је под 5, atoi.


Питање: Дат је кôд функције funkcija() написане у програмском језику C. Изабрати којој стандарднoj функцији одговара дата функција.

char * funkcija(char *s) 
{
char c,*temp;
temp=s;
while((c=getchar())!='\n')*temp++=c;
*temp='\0';
return s;
}

1. isupper
2. isalpha
3. gets
4. strncat
5. atoi
6. strchr
7. strcmp

Одговор: Тачан одговор је под 3, gets.


Питање: Дат је кôд функције funkcija() написане у програмском језику C. Анализирати кôд и одредити којој стандардној функцији одговара дата функција.

int funkcija(char *s, char *t) 
{
char tempt, temps;
while(*s && *t){
if(*t>='A'&& *t<='Z') tempt = 'a' + *t -'A';
else tempt=*t;
if(*s>='A'&& *s<='Z') temps = 'a' + *s -'A';
else temps=*s;
if(temps != tempt) return temps - tempt;
else s++, t++;
}
return *s - *t; .
}

1. isupper
2. isalpha
3. gets
4. strncat
5. atoi
6. strchr
7. strcmp

 Одговор: Тачан одговор је под 7, strcmp.
Питање: На програмском језику С, декларисани су стрингови:

char s1[100]="", s2[100]="geografija";
char *t="nacrtna geometrija";

Одредити вредност стринга по извршењу наведене наредбе (наредбе не посматрати као секвенцу, већ независно једну од друге):

1. strcpy(s1, t); 		s1=
2. strncpy(s1, t, 4);	 	s1=
3. strcpy(s2, t); 		s2=
4. strncpy(s2,t+9,3); 		s2=

Одговор: 
Под 1, вредност s1=nacrtna geometrija
Под 2, вредност s1=nacr
Под 3, вредност s2= nacrtna geometrija
Под 4, вредност s2=eomgrafija

Питање: Нa програмском језику C дат је програм:

#include<stdio.h>
#include <string.h>
main()
{
char s1[]="Kratka Servisna Poruka", *s2, *s3;
s2=strchr(s1,'S');
s3=strrchr(s2,'P');
strncpy(s1+1,s2,1);
strcpy(s1+2,s3);
puts(s1);
puts(s2);
puts(s3);
}

Одредити шта приказују наредбе puts(s1);puts(s2); puts(s3); односно шта је садржај стрингова s1, s2, s3 по извршењу програма:
Одговор:

s1= KSPoruka
s2= a
s3= Poruka

На Петљи можете решавати задатке из Методичке збирке задатака из основа програмирања, део „Матрице“, који се налазе на линку Metodicka zbirka zadataka користећи онлајн С или С/С++ компајлер.
За почетак пробајте да решите задатак из збирке који се налази на линку Prezime pa ime. 


--->