# Увод

Шта ћеш научити 

- да разликујеш низ од стринга
- да примениш технике рада са низовима на стрингу 
- да пишеш програме за унос, формирање и приказ стринга
- да претражујеш стринг
- да користиш готове функције за рад са стрингом 
- да користиш стрингове у функцијама
- да примениш адресну аритметику показивача над стрингом 

Да се подсетимо градива из Програмирања 1. 

У програмима, поред нумеричких података, често се јавља потреба за рад са текстом. Већина програмских језика поседује посебне типове променљивих за представљање знакова или низова знакова који чине текст.

Као што смо научили у првом разреду, у С језику постоје само нумерички типови података. Један од целобројних типова података char намењен је за приказ карактера. То значи да сваки карактер има свој кôд, чији приказ зависи од начина конверзије.
Ако је дата променљива `int a = 65`; наредба `printf("%d", a)` на излазу ће дати број 65, док ће наредба `printf("%c", 65)` на излазу дати карактер А. 

Осим знака постоји и знаковна константа која се од знака разликује по томе што, осим знака, садржи још један знак који се зове `null` карактер. `Null` је карактер са вредношћу 0, a *ascii* вредност `null` карактера може се писати и као `'\0'`.Неки га још називају празним знаком. 
Знаковна константа се пише између знакова навода.

Значи, 'А' и "А" се разликују у томе што се "А" састоји из два карактера – 'А' '\0' .



