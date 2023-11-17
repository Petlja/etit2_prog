
# Библиотеке и функције за рад са стрингом 

Библиотечке функције за рад са стринговима налазе се у неколико библиотека:

- `stdio.h`

- `string.h`

- `stdlib.h`

Функције за рад са знаковима налазе се у библиотеци:

- `ctype.h`

Размотрићемо редом једну по једну библиотеку. 


## Библиотека `<stdio.h>`

Упознали смо се са функцијама за унос знакова и стрингова.

Да се подсетимо:

- Форматирани унос знака реализује се функцијом `scanf` уз конверзију `%c`.
- Неформатирани унос знака реализује се функцијом `getchar()`. 
- Форматирани унос стринга реализује се функцијом `scanf` уз примену конверзије `%s`. 
- Неформатирани унос стринга реализује се функцијом `gets(s)`.
- Форматирани испис знакова реализује се функцијом `printf` уз примену конверзије `%c`.
- Неформатирани испис знака реализује се функцијама `putchar(c)`.
- Форматирани испис стринга реализује се функцијом `printf` уз примену конверзије `%s`.
- Неформатирани испис стринга реализује се функцијом `puts(s)`.

Све наведене функције налазе се у библиотеци `stdio.h`.

## Библиотека `<string.h>`

У С језику не постоји ни један оператор за обраду стрингова.
За операције са стринговима користе се функције у библиотеци <string.h>.
У следећој табели t и s су низови знакова – стрингови, n је целобројни податак, c је карактер.

```{image} images/image7.png
:width: 550
:align: center
```

Напишимо и анализирајмо функцију по функцију.

Функција `strlen(s)` враћа дужину низа знакова `s` (`\0` се не убраја). Резултат је типа `int`.

```c
//Primer strlen
#include <stdio.h>
#include <string.h>
int main(void)
{
    char s[256];
    printf ("Unesite tekst: ");
    gets(s);
    printf ("Uneto je %u znakova\n", strlen(s));
    return 0;
}
```

Излаз: 

```text
Unesite tekst: Ovo je tekst unet sa konzole
Uneto je 28 znakova
```

Функција `strcpy(t, s)` преписује (копира) знаковни низ низа знакова `s` у низ знакова `t` укључујући и `\0`.


```c
//Primer strcpy
#include <stdio.h>
#include <string.h>
int main(void)
{
    char s[] = "Sadrzaj stringa za kopiranje";
    char t[40];
    char str[40];
    strcpy(t,s);
    printf ("Pocetni string s: %s\nKopirani string t: %s\n ", s, t);
    return 0;
}
```

 Излаз:

 ```text
Pocetni string s: Sadrzaj stringa za kopiranje
Kopirani string t: Sadrzaj stringa za kopiranje
```

Функција `strncpy(t,s,n)` преписује највише n знакова из низа знакова `s` у низ знакова `t`. Ако `s` нема `n` знакова, допуњује се са `\0` до дужине `n`.

```c
//Primer 1 strncpy 
#include <stdio.h>
#include <string.h>
int main(void)
{
char s[]= "To be or not to be";
char t[40]="String t pre kopiranja";
printf("Sadrzaj stringa t pre kopiranja je:\n");
puts(t);
strncpy (t,s,10);
printf("Sadrzaj stringa t posle kopiranja je:\n");
puts(t);
return 0;
}
```

Излаз:

```text
Sadrzaj stringa t pre kopiranja je:
String t pre kopiranja
Sadrzaj stringa t posle kopiranja je:
To be or nre kopiranja
```

Ако у стринг `t` додамо завршни знак '\0' на индексу добићемо:

```c
//Primer 2 strncpy 
#include <stdio.h>
#include <string.h>
int main(void)
{
    char s[] = "To be or not to be";
    char t[40] = "String t pre kopiranja";
    printf("Sadrzaj stringa t pre kopiranja je:\n");
    puts(t);
    strncpy (t, s, 10);
    t[10] = '\0';
    printf("Sadrzaj stringa t posle kopiranja je:\n");
    puts(t);
    return 0;
}
```

Излаз:

```text
Sadrzaj stringa t pre kopiranja je:
String t pre kopiranja
Sadrzaj stringa t posle kopiranja je:
To be or n
```

Функција `strcat(t, s)` дописује низ знакова `s` на крај низа знакова `t`.

```c
//Primer strcat
#include <stdio.h>
#include <string.h>
int main(void)
{
char t[80];
    strcpy(t, "Stringovi ");
    strcat(t, "su ");
    strcat(t, "spojeni.");
    puts(t);
    return 0;
}
```

Излаз:

```text
Stringovi su spojeni.
```

Функција `strcat(t, s, n)` дописује највише `n` знакова из низа знакова `s` у низ знакова `t`.

```c
//Primer strncat
#include<stdio.h>
#include<string.h>
int main(void)
{
    char t[20] = "To be ";
    char s[20] = "or not to be";
    strncat (t, s, 6);
    puts (t);
    return 0;
}
```

Излаз:

```text
To be or not
```

Функција `strcmp(t, s)` упоређује низове знакова `t` и `s`. Вредност је негативна ако је `t` мање од `s`. Вредност је позитивна ако је `t` веће од `s`. Вредност је `0` ако су стрингови исти. Тип резултата је `int`. Упоређивање се врши знак по знак из `ascii` табеле.

```{image} images/image8.png
:width: 550
:align: center
```

```c
//Primer strcmp 
#include<stdio.h>
#include<string.h>
int main(void)
{
    char Resenje[] = "kruska";
    char Odgovor[80];
    do 
    {
        printf("Koje je moje omiljeno voce? ");
        gets(Odgovor);
    } 
    while(strcmp(Resenje, Odgovor) != 0);
    printf("\nOdgovor je tacan!\n");
    return 0;
}
```

Излаз:

```text
Koje je moje omiljeno voce? Jabuka
Koje je moje omiljeno voce? Sljiva
Koje je moje omiljeno voce? Kruska
Koje je moje omiljeno voce? kruska

Odgovor je tacan!
```

Функција `strncmp(t, s, n)` упоређује `n` првих знакова у стрингу `t` и `s`. Резултат се образује као и код функције `strcmp`. Тип резултата је `int`.

```c
//Primer strncmp
#include<stdio.h>
#include<string.h>
int main(void)
{
    char t[40], s[40];
    int n;
    printf ("Unesi prvi string t: ");
    gets(t);
    printf("Unesi drugi string s: ");
    gets(s);
    printf ("Unesi broj karaktera za poredjenje: ");
    scanf("%d", &n);
    if(strncmp(t, s, n) == 0)
        printf("Prvih %d znakova stringa %s i %s su isti", n, t, s);
    else
        printf("Prvih %d znakova stringa %s i %s nisu isti", n, t, s);
    return 0;
}
```

Излаз 1:

```text
Unesi prvi string t: Novi Sad
Unesi drugi string s: Novi Beograd
Unesi broj karaktera za poredjenje: 5
Prvih 5 znakova stringa Novi Sad i Novi Beograd su isti
```

Излаз 2:

```text
Unesi prvi string t: Novi Sad
Unesi drugi string s: Novi Beograd
Unesi broj karaktera za poredjenje: 6
Prvih 6 znakova stringa Novi Sad i Novi Beograd nisu isti
```

```{questionnote}
Шта примећујете?
```

Функција `strchr(t, c)` – вредност ове функције је показивач `(char*)` на први елеменат стринга који садржи знак `c`. Ако нема знака c у стрингу, резултат је `NULL`.

```c
//Primer strchr
#include<stdio.h>
#include<string.h>
int int main(void)
{
    char t[] = "Ovo je test recenica";
    char *c;
    printf ("Trazim karakter 'e' u \"%s\"...\n", t);
    c = strchr(t, 'e');
    while (c != NULL)
    {
        printf ("pronasao sam 'e' na poziciji %d\n", c - t + 1);
        c = strchr(c+1, 'e');
    }
    return 0;
}
```

Излаз:

```text
Trazim karakter 'e' u "Ovo je test recenica"...
pronasao sam 'e' na poziciji 6
pronasao sam 'e' na poziciji 9
pronasao sam 'e' na poziciji 14
pronasao sam 'e' na poziciji 16
```

Функција `strrchr(t, c)` - вредност ове функције је показивач `(char*)` на задњи елеменат стринга који садржи знак `c`. Ако нема знака c у стрингу, резултат је `NULL`.

```c
//Primer strrchr
#include<stdio.h>
#include<string.h>
int int main(void)
{
    char * c;
    c = strrchr(t, 'e');
    printf ("Poslednja pojava karaktera 'e' je na poziciji %d\n", c - t + 1);
    return 0;
}
```

Излаз:

```text
Poslednja pojava karaktera 'e' je na poziciji 16
```

Функција `strstr(t, s)` у стрингу `t` налази подстринг `s`. Ако је подстринг нађен, показивач се враћа на прво појављивање, а ако није враћа се `NULL`.

```c
//Primer strstr
#include<stdio.h>
#include<string.h>
int int main(void)
{
    char t[] = "Ovo je jedan primer";
    char *c;
    c = strstr(t, "dan");
    printf("Pronadjena pozicija je %d\n", c - t + 1);
    return 0;
}
```

Излаз:

```text
Pronadjena pozicija je 10
```

## Библиотека <stdlib.h>

Уколико желимо да стринг конвертујемо у нумеричку вредност, користимо функције које се налазе у библиотеци `stdlib.h.`
Овде ћемо обрадити следеће функције:  

```{image} images/image9.png
:width: 550
:align: center
```

Функција `atof(s)` врши конверзију реалног броја из низа цифара облика ccc.cccEee у бинарни еквивалент. Аргумент `s` је стринг, а повратна вредност функције је `double`.

```c
//Primer atof
#include<stdio.h>
#include<stdlib.h>
#include<math.h>
int main(void)
{
    double n, m;
    double pi = 3.1415926535;
    char s[256];
    printf("Unesite vrednost u stepenima: ");
    gets(s);
    n = atof(s);
    m = sin(n*pi/180);
    printf("sin(%f) je %f\n" , n, m);
    return 0;
}
```

Излаз:

```text
Unesite vrednost u stepenima: 45
sin(45.000000) je 0.707107
```

Функција `atoi(s)` врши конверзију целог броја из низа цифара облика cccc у бинарни еквивалент. Аргумент `s` је стринг, а повратна вредност функције је `int`. Конверзија се врше све док је могуће конвертовати вредност у цео број, као што ћете видети у примерима. 

```c
//Primer atoi
#include<stdio.h>
#include<stdlib.h>
int main(void)
{
    int i;
    char s[256];
    printf ("Unesite broj: ");
    gets(s);
    i = atoi(s);
    printf ("Uneta vrednost je %d, a njena dvostruka vrednost je %d\n", i, i * 2);
    return 0;
}
```

Излаз 1:

```text
Unesite broj: 256
Uneta vrednost je 256, a njena dvostruka vrednost je 512
```

Излаз 2:

```text
Unesite broj: 25.3658
Uneta vrednost je 25, a njena dvostruka vrednost je 50
```

Излаз 3:

```text
Unesite broj: ab256
Uneta vrednost je 0, a njena dvostruka vrednost je 0
```

Функција `atol(s)` врши конверзију целог броја из низа цифара облика cccc у бинарни еквивалент. Аргумент `s` је стринг, а повратна вредност функције је `long int`.

```c
//Primer atol
#include<stdio.h>
#include<stdlib.h>
int main(void)
{
    long i;
    char s[256];
    printf("Unesite broj: ");
    gets(s);
    i = atol(s);
    printf("Uneta vrednost je %ld, a njena dvostruka vrednost je %ld\n", i, i * 2);
}
```

Излаз: 

```text
Unesite broj: 123456789
Uneta vrednost je 123456789, a njena dvostruka vrednost je 246913578
```

## Библиотека <ctype.h>

С обзиром да је стринг низ карактера, понекад је потребно проверавати карактере и то користити за решавање проблема. За испитивање знакова користе се функције у библиотеци `<ctype.h>`. Оне испитују у коју категорију спада знак `c`.

```{image} images/image10.png
:width: 600
:align: center
```
Функција `isalnum(c)` проверава да ли је знак `c` слово или цифра. 

```{questionnote}
Написати програм који ће за сваки знак од 0 до 127 из ascii табеле проверити да ли је знак слово или цифра.

```
**Решење**

```c
#include <ctype.h>
#include <stdio.h>
int main(void)
{
    short int i;
    for (i = 0; i < 128; i++)
        if (isalnum(i))
            printf("isalnum (%c) \t Da \n", i);
        else
            printf("isalnum (%c)\t Ne\n", i);
    return 0;
}
```
Излаз:
```text
isalnum (.)      Ne
isalnum (/)      Ne
isalnum (0)      Da
isalnum (1)      Da
...
isalnum (9)      Da
isalnum (:)      Ne
isalnum (;)      Ne
...
isalnum (?)      Ne
isalnum (@)      Ne
isalnum (A)      Da
isalnum (B)      Da
...
isalnum (D)      Da
isalnum (E)      Da
...
```
Функција `isalpha(c)` проверава да ли је знак `с` слово. 

```{questionnote}
Написати програм који ће за сваки карактер од 0 до 127 из ascii табеле проверити да ли је тај знак слово.

```
**Решење**

```c
#include <ctype.h>
#include <stdio.h>
int main(void)
{
    short int i;
    for (i = 0; i < 128; i++)
        if (isalnum(i))
            printf("isalnum (%c) \t Da \n", i);
        else
            printf("isalnum (%c)\t Ne\n", i);
    return 0;
}
```
Излаз:
```text
...
isalpha (<) Ne
isalpha (=) Ne
isalpha (>) Ne
isalpha (?) Ne
isalpha (@) Ne
isalpha (A) Da
isalpha (B) Da
isalpha (C) Da
...
```
Функција `isdigit(c)` проверава да ли је знак `c` цифра.
```{questionnote}
Написати програм који ће за сваки знак од 0 до 127 из ascii табеле проверити да ли је тај знак цифра.
```
**Решење**

```c
#include <ctype.h>
#include <stdio.h>
int main(void)
{
    short int i;
    for (i = 0; i < 128; i++)
    {
        if(isdigit(i))
            printf("isdigit (%c) Da \n", i);
        else
            printf("isdigit (%c) Ne\n", i); 
    }
    return 0;
}
```
Излаз:
```text
...
isdigit (,) Ne
isdigit (-) Ne
isdigit (.) Ne
isdigit (/) Ne
isdigit (0) Da
isdigit (1) Da
isdigit (2) Da
...
isdigit (8) Da
isdigit (9) Da
isdigit (:) Ne
isdigit (;) Ne
isdigit (<) Ne
...
```
Функција `islower(c)` проверава да ли је знак `c` мало слово.
```{questionnote}
Написати програм који ће за сваки знак од 0 до 127 из ascii табеле проверити да ли је тај знак мало слово.
```
**Решење**

```c
#include <ctype.h>
#include <stdio.h>
int main(void)
{
    short int i;
    for (i = 0; i < 128; i++)
    {
        if(islower(i))
            printf("islower(%c) Da \n", i);
        else
            printf("islower(%c) Ne\n", i);
    }
    return 0;
}
```
Излаз:
```text
...
islower(U) Ne
islower(V) Ne
...
islower(Y) Ne
islower(Z) Ne
islower([) Ne
...
islower(_) Ne
islower(`) Ne
islower(a) Da
islower(b) Da
islower(c) Da
islower(d) Da
islower(e) Da
...
```
Функција `isupper(c)` проверава да ли је знак `c` велико слово.
```{questionnote}
Написати програм који ће за сваки знак од 0 до 127 из ascii табеле проверити да ли је тај знак велико слово.
```
**Решење**

```c
#include <ctype.h>
#include <stdio.h>
int main(void)
{
    short int i;
    for (i = 0; i < 128; i++)
    {
        if(isupper(i))
            printf("isupper(%c) Da \n", i);
        else
            printf("isupper(%c) Ne\n", i);
    }
    return 0;
}
```
Излаз:
```text
...
isupper(S) Da
isupper(T) Da
isupper(U) Da
isupper(V) Da
isupper(W) Da
isupper(X) Da
isupper(Y) Da
isupper(Z) Da
isupper([) Ne
...
isupper(_) Ne
isupper(`) Ne
isupper(a) Ne
isupper(b) Ne
isupper(c) Ne
...
```
Функција `isspace(c)` проверава да ли је знак `c` бели знак.
```{questionnote}
Написати програм који ће за сваки знак од 0 до 127 из ascii табеле проверити да ли је тај знак бели знак.
```
**Решење**

```c
#include <ctype.h>
#include <stdio.h>
int main(void)
{
    short int i;
    for (i = 0; i <128; i++)
    {
        if(isspace(i))
            printf("isspace(%c) Da \n", i);
        else
            printf("isspace(%c) Ne\n", i);
    }
    return 0;
}
```
Излаз:
```text
...
isspace(∟) Ne
isspace(↔) Ne
isspace(▲) Ne
isspace(▼) Ne
isspace( ) Da
isspace(!) Ne
isspace(") Ne
isspace(#) Ne
isspace($) Ne
isspace(%) Ne
isspace(&) Ne
...
```
Функција `iscntrl(c)` проверава да ли је знак `c` управљачки или контролни знак.
```{questionnote}
Написати програм који ће за сваки знак од 0 до 127 из ascii табеле проверити да ли је тај знак управљачки или контролни знак.
```
**Решење**

```c
#include <ctype.h>
#include <stdio.h>
int main(void)
{
    short int i;
    for (i = 0; i <128; i++)
    {
        if(iscntrl(i))
            printf("iscntrl(%d-%c) Da \n", i,i);
        else
            printf("iscntrl(%d-%c) Ne\n", i,i);
    }
    return 0;
}
```
Излаз:
```text
...
scntrl(23-↨) Da
iscntrl(24-↑) Da
iscntrl(25-↓) Da
iscntrl(26-→) Da
iscntrl(27-←) Da
iscntrl(28-∟) Da
iscntrl(29-↔) Da
iscntrl(30-▲) Da
iscntrl(31-▼) Da
iscntrl(32- ) Ne
iscntrl(33-!) Ne
iscntrl(34-") Ne
iscntrl(35-#) Ne
iscntrl(36-$) Ne
iscntrl(37-%) Ne
...
```
Функција `ispunct(c)` проверава да ли је знак `c` специјални знак.
```{questionnote}
Написати програм који ће за сваки знак од 0 до 127 из ascii табеле проверити да ли је тај знак специјални знак.
```
**Решење**

```c
#include <ctype.h>
#include <stdio.h>
int main(void)
{
    short int i;
    for (i = 0; i <128; i++)
    {
        if(ispunct(i))
            printf("ispunct(%d-%c) Da \n", i,i);
        else
            printf(" ispunct(%d-%c) Ne\n", i,i);
    }
    return 0;
}
```
Излаз:
```text
...
ispunct(42-*) Da
ispunct(43-+) Da
ispunct(44-,) Da
ispunct(45--) Da
ispunct(46-.) Da
ispunct(47-/) Da
ispunct(48-0) Ne
ispunct(49-1) Ne
ispunct(50-2) Ne
ispunct(51-3) Ne
ispunct(52-4) Ne
ispunct(53-5) Ne
...
```

Функција `isxdigit(c)` проверава да ли је знак `c` хексадецимални број.
```{questionnote}
Написати програм који ће за сваки знак од 0 до 127 из ascii табеле проверити да ли је тај знак хексадецимални број.
```
**Решење**

```c
#include <ctype.h>
#include <stdio.h>
int main(void)
{
    short int i;
    for (i = 0; i < 128; i++)
    {
        if(isxdigit(i))
            printf("isxdigit (%c) Da \n", i);
        else
            printf("isxdigit (%c) Ne\n", i); 
    }
    return 0;
}
```
Излаз:
```text
...
isxdigit (7) Da
isxdigit (8) Da
isxdigit (9) Da
isxdigit (:) Ne
isxdigit (;) Ne
...
isxdigit (?) Ne
isxdigit (@) Ne
isxdigit (A) Da
isxdigit (B) Da
isxdigit (C) Da
isxdigit (D) Da
isxdigit (E) Da
isxdigit (F) Da
isxdigit (G) Ne
isxdigit (H) Ne
isxdigit (I) Ne
isxdigit (J) Ne
...
```
Функција `isgraph(c)` проверава да ли је знак `c` штампајући знак, али не и размак
```{questionnote}
Написати програм који ће за сваки знак од 0 до 127 из ascii табеле проверити да ли је тај знак штампајући знак, али не и размак.
```
**Решење**

```c
#include <ctype.h>
#include <stdio.h>
int main(void)
{
    short int i;
    for (i = 0; i < 128; i++)
    {
        if(isgraph(i))
            printf("isgraph(%c) Da \n", i);
        else
            printf("isgraph(%c) Ne\n", i); 
    }
    return 0;
}
```
Излаз:
```text
...
isgraph(↓) Ne
isgraph(→) Ne
isgraph(←) Ne
isgraph(∟) Ne
isgraph(↔) Ne
isgraph(▲) Ne
isgraph(▼) Ne
isgraph( ) Ne
isgraph(!) Da
isgraph(") Da
isgraph(#) Da
isgraph($) Da
isgraph(%) Da
isgraph(&) Da
...
```
Функција `isprint(c)` проверава да ли је знак `c` штампајући знак, укључујући и размак
```{questionnote}
Написати програм који ће за сваки знак од 0 до 127 из ascii табеле проверити да ли је тај знак штампајући знак, укључујући и размак.
```
**Решење**

```c
#include <ctype.h>
#include <stdio.h>
int main(void)
{
    short int i;
    for (i = 0; i < 128; i++)
    {
        if(isprint(i))
            printf("isprint(%c) Da \n", i);
        else
            printf("isprint(%c) Ne\n", i); 
    }
    return 0;
}
```
Излаз:
```text
...
isprint(↓) Ne
isprint(→) Ne
isprint(←) Ne
isprint(∟) Ne
isprint(↔) Ne
isprint(▲) Ne
isprint(▼) Ne
isprint( ) Da
isprint(!) Da
isprint(") Da
isprint(#) Da
isprint($) Da
isprint(%) Da
isprint(&) Da
...
```
Осим горе наведених функција, за испитивање знакова користе се и функције за конверзију у библиотеци `<ctype.h>`.
Овде иде слика!!!!!!!!!!!!

Уколико карактер с није слово, повратна вредност је карактер с.
Функција `tolower(c)` уколико је карактер `с` велико слово конвертује га у мало – у супротном, повратна вредност је сâм карактер `с`.
```{questionnote}
Написати програм који ће сваки знак од 32 до 127 из ascii табеле конвертовати – велика слова у мала.
```
**Решење**

```c
#include <ctype.h>
#include <stdio.h>
int main(void)
{
    unsigned char i;
    for (i = 0x20; i < 0x7F; i++) /* od 32 do 127*/
        printf ("tolower(%c) = %c\n", i, tolower(i));
    return 0;
}
```
Излаз:
```text
...
tolower(T) = t
tolower(U) = u
tolower(V) = v
tolower(W) = w
tolower(X) = x
tolower(Y) = y
tolower(Z) = z
tolower([) = [
tolower(\) = \
...
tolower(`) = `
tolower(a) = a
tolower(b) = b
tolower(c) = c
tolower(d) = d
tolower(e) = e
tolower(f) = f
...
```
Функција `toupper(c)` уколико је карактер `с` уколико је карактер с мало слово, конвертује га у велико – у супротном, повратна вредност је сâм карактер `с`.
```{questionnote}
Написати програм који ће сваки знак од 32 до 127 из ascii табеле конвертовати – мала слова у велика.
```
**Решење**

```c
#include <ctype.h>
#include <stdio.h>
int main(void)
{
    unsigned char i;
    for (i = 0x20; i < 0x7F; i++) /* od 32 do 127*/
        printf ("toupper(%c) = %c\n", i, toupper(i));
    return 0;
}
```
Излаз:
```text
...
toupper(W) = W
toupper(X) = X
toupper(Y) = Y
toupper(Z) = Z
toupper([) = [
toupper(\) = \
toupper(]) = ]
toupper(^) = ^
toupper(_) = _
toupper(`) = `
toupper(a) = A
toupper(b) = B
toupper(c) = C
toupper(d) = D
toupper(e) = E
toupper(f) = F
toupper(g) = G
...
```




