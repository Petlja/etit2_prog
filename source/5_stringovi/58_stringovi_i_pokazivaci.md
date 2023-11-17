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
