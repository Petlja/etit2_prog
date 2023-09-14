# Унос и испис стринга 

Као и код карактера, унос и испис стринга може да се врши на два начина:

- са конверзијом (форматирани унос и испис), и
- без конверзије (неформатирани унос и испис). 

## Унос стринга 

Форматирани унос стринга (са конверзијом) реализује се функцијом `scanf` уз примену конверзије `%s`.
Читање почиње од првог небелог знака и завршава се када се наиђе на први бео знак.

Посматрајмо следеће линије кода:

```text
1. char ime[51], prezime[51];
2. char *sifra;
3. sifra = (char*)calloc(100, sizeof(char));
4. scanf(“%s%s”, ime, prezime);
5. scanf(“%s”, sifra);
```

У линији 1 су ime и prezime променљиве типа `string`, у које може да се смести максимално 50 карактера + 1 `null` карактер.

Линија 2 дефинише показивач на низ знакова.

Линија 3 резервише адресну локацију за 100 елемената, од којих је сваки величине за податак типа `char`.

Линије 4  и 5 учитавају податак са стандардног улаза и прослеђују га конверзијом као стринг у променљиве `ime`, `prezime` и `sifra`.

Неформатирани унос стринга (без конверзије) реализује се функцијом `gets(s)`.

Ова функција са главног улаза (тастатуре) чита један ред текста, до знака за прелаз у нови ред, и смешта га у стринг `s`.

Уместо знака `'\n'` којим се завршава ред, на крај низа се ставља знак `'\0'`.

Ако је читање успешно, функција `gets` враћа почетну адресу стринга `s`, а ако је читање неуспешно, враћа симболичку константу `NULL`.


Посматрајмо следеће линије кода:

```text
1. char s1[100], *s2; 
2. s2 = malloc(100 * sizeof(char));
3. gets(s1);
4. gets(s2);
```

Линија 1 дефинише променљиве типа стринг класично, односно преко показивача.

Линија 2 резервише меморијски простор за стринг `s2`.

Линијама 3 и 4 врши се учитавање вредности са стандардног улаза и прослеђивање променљивој `s1` односно `s2` без конверзије.

## Испис стринга 

Форматирани испис стринга (са конверзијом) реализује се функцијом `printf` уз примену конверзије `%s`.
Исписују се сви знакови, укључујући и беле знакове, до празног знака `'\0'`.
Посматрајмо следеће линије кода:

```text
1. printf(“%s_%s”,);
2. printf(“%20s”, ime);
3. printf(“%-20s”, ime);
4. printf(“%20.15s”, ime);
```

Линија 1 исписује на стандардном излазу вредности променљивих `ime` и `prezime`, раздвојене доњом цртом.

Линија 2 исписује на стандардном излазу вредност променљиве ime на 20 позиција, а ако је име краће од 20 допуњује се бланко знацима испред текста.

Линија 3 исписује на стандардном излазу вредност променљиве ime на 20 позиција уз леву ивицу, а ако је име краће од 20 допуњује се бланко знацима иза текста.

Линија 4 исписује на стандардном излазу вредност променљиве ime на 20 позиција, а ако је име краће од 20 допуњује се бланко знацима иза текста. 15 представља највећи број знакова за исписивање. Ако је текст дужи, онда се вишак не исписује.

Неформатирани испис стринга (без конверзије) реализује се функцијом `puts(s)`.

Ова функција на главни излаз (монитор) исписује садржај стринга s и уместо завршног знака `'\0'` додаје знак за прелаз у нови ред `'\n'`.

Ако текст у стрингу садржи знакове `'\n'`, резултат ће бити више исписаних редова.

Ако је писање успешно, функција puts враћа број исписаних карактера, а ако је писање неуспешно враћа се симболичка константа `EOF`.

```text
1. char s1[100], *s2;
2. puts(s1);
3. puts(s2);
```

Линија 1 дефинише променљиве типа стринг класично, односно преко показивача.

Линијама 2 и 3 врши се исписивање вредности променљивих `s1` односно `s2` на стандардном излазу без конверзије.

```{questionnote}
Написати програме за унос и испис имена и презимена са и без конверзије.
```

**Решење**:

- са конверзијом

```c
#include <stdio.h>
int main(void) {
    char ime_prezime[40];
    printf("Unesi ime i prezime: ");
    scanf("%s", ime_prezime);
    printf("Uneli ste ime i prezime sa konverzijom %s",ime_prezime);
    return 0;
}
```

Излаз:

```text
Unesi ime i prezime: Petrovic Mitrovic Petar
Uneli ste ime i prezime sa konverzijom Petrovic
Унети су карактери до прве празнине – без конверзије.
```
```c
#include <stdio.h>
int main(void) {
    char ime_prezime[40];
    printf("Unesi ime i prezime ");
    gets(ime_prezime);
    printf("Uneli ste ime i prezime bez konverzije %s",ime_prezime);
    return 0;
}
```

Излаз:

```text
Unesi ime i prezime Petrovic Mitrovic Petar
Uneli ste ime i prezime bez konverzije Petrovic Mitrovic Petar
```

Унети су сви карактери до ентера.

```{questionnote}
Написати програм који демонстрира форматирани излаз стринга. 
```

**Решење**:

```c
//Primer 1
#include <stdio.h>
int main(void) 
{
    char ime[]="Pera", prezime[]="Peric";
    printf ("Ime je %s %s", ime,prezime);
    return 0;
}
```

Излаз:

Ime je Pera Peric

```c
//Primer 2
#include <stdio.h>
int main(void) 
{
    char ime[]="Pera", prezime[]="Peric";
    printf ("Ime je %20.15s %30.15s", ime,prezime);
    return 0;
}
```

Излаз:

Ime je         Pera             Peric

```c
//Primer 3
#include <stdio.h>
int main(void) 
{
    char ime[]="Pera", prezime[]="Peric";
    printf ("Ime je %20.3s %30.4s", ime,prezime);
    return 0;
}
```

Излаз:

Ime je         Per              Peri

Напишите следећи програм:

```c
#include <stdio.h>
int main(void) {
    char poruka1[] = "Zdravo svete 1";
    char *poruka2 = "Zdravo svete 2";
    printf("Formatirani izlaz:\n");
    printf("Poruka 1: %s\n", poruka1);
    printf("Poruka 2: %s", poruka2);
    printf("\n\n");
    printf("Neformatirni izlaz:\n");
    puts(poruka1);
    puts(poruka2);
    printf("\n\n");
    printf("Prikaz dela stringa:\n");
    printf("%s\n", poruka1 + 3);
    puts(poruka2 + 8);
    return 0;
}
```

Излаз:

```text
Formatirani izlaz:
Poruka 1: Zdravo svete 1
Poruka 2: Zdravo svete 2

Neformatirni izlaz:
Zdravo svete 1
Zdravo svete 2

Prikaz dela stringa:
avo svete 1
vete 2
```