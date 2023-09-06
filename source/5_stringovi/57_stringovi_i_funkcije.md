# Стрингови и функције

С обзиром да су стрингови низови карактера који се завршавају празним знаком, приликом употребе у функцијама понашају се идентично као низови. Да бисмо ово боље разумели, урадићемо неколико задатака.

```{questionnote}
Написати програм који ће учитати стринг `s` и карактер `x` и исписати колико пута се тај карактер појављује у том стрингу. 
Користити функцију `broj_karaktera(char x, char s[])`;
```

**Решење**:

```c
#include <stdio.h>
#include <string.h>
int broj_karaktera(char x, char s[])
{ 
    int i, br = 0;
        for (i = 0; i < strlen(s); i++)
            if (s[i] == x) br++;
    return br;
}

int main(void)
{
    char x, str[50];
    printf("\nProgram broji pojavljivanje nekog slova u stringu\n");
    printf("\nUnesite string: \n");
    gets(str);
    printf("\nUnesite slovo: ");
    scanf("%c", &x);
    printf("Slovo '%c' se u stringu pojavljuje %d puta", x, broj_karaktera(x, str));
    return 0;
}
```
Излаз:

```text
Program broji pojavljivanje nekog slova u stringu

Unesite string:
Ana voli Milovana

Unesite slovo: a
Slovo 'a' se u stringu pojavljuje 3 puta
```

```{questionnote}
Написати функцију за испитивање да ли је нека ниска палиндром. Програм треба да прочита једну реч без размака, испита да ли је палиндром, испише резултат и понавља претходне кораке све док не прочита реч која почиње тачком. Користити функцију `palindrom(rec)`.
```

```{suggestionnote}
Палиндром је ниска која се исто чита у оба смера. 
```

```c
#include <stdio.h>
#include <string.h>
int palindrom (char n[])
{
    int i, j;
    for(i = 0, j = strlen(n) - 1; i < j; i++, j--)
        if(n[i] !=n [j]) 
            return 0;
    return 1;
}

int main(void)
{
    char rec[50];
    while(1)
    {
        printf("Unesi rec: \n");
        scanf("%s", rec);
            if (rec[0] == '.')
                break;
        printf("%s palindrom\n\n", (palindrom(rec) ? "\nJeste" : "\nNije"));
    }
    return 0;
}
```

Излаз:

```text
Unesi rec:
Ana

Nije palindrom

Unesi rec:
ana

Jeste palindrom


