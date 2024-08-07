
Назовем это общей теорией

Можем начать с машинного языка. 
Машинный язык (или машинный код) - это самый низкоуровневый язык программирования, который понимает компьютерное устройство напрямую. В машинном языке команды представлены в виде двоичных чисел, которые интерпретируются процессором компьютера.

Бит -  Один или ноль. Есть сигнал или нет 
1 байт = 8 бит [  ]  [  ]  [  ]  [  ]  [  ]  [  ]  [  ]  [  ]
Пример записи информации в 1 байт = 1010 0001 = A1 
т.е. два блока по 4 бита в которые записан шестнадцатеричный символ. 

```
B8 0A 00
```

Машинный язык прямо связан с архитектурой конкретного процессора. Каждый тип процессора имеет свой набор инструкций и формат представления команд. Например, для процессоров архитектуры x86 команды представлены в виде набора двоичных кодов определенной длины.

Мнемоника в языке ассемблера представляет собой набор символов или ключевых слов, которые используются для представления машинных команд процессора. Мнемоника обычно выбирается таким образом, чтобы легко запомнить и понять, что делает конкретная инструкция.

Например, мнемоника `MOV` используется для инструкции перемещения данных, `ADD` - для инструкции сложения, `SUB` - для инструкции вычитания и так далее. Каждая мнемоника обычно сопровождается операндами, которые указывают, над какими данными выполняется операция.

```
MOV AX, BX   ; Перемещение данных из регистра BX в регистр AX
ADD AX, 10   ; Сложение значения в регистре AX с константой 10
SUB CX, DX   ; Вычитание значения в регистре DX из регистра CX
```
Далее программа написанная на мнемонике переводится на машинный язык который будет понятен процессору с помощью компилятора. 

Язык С написан программистами для программистов, чтобы уйти от Ассемблера и писать на более высоком уровне абстракции. Но при этом он сохраняет плюсы низкоуровневого языка при написании программы - свободу и контроль. 

Программы написанные на С  эффективно переводятся на машинный язык и быстро работают. 

В операционной системе Пользовательские программы взаимодействуют с драйверами через системные запросы 

т.е  в 1 байте можем представить числа в пределах [0 ; 255] или если брать "беззнаковые" и [-128;127] для "знаковых" 

Используются [[Модификаторы типов данных С]]
```C
unsigned int x; 
// беззнаковый. x может принимать только неотрицательные значения
signed int y;
// знаковый. y может принимать отрицательные и положительные значения

// только для целоцисленных типов данных и они по умолчанию знаковые
// Осторожнее с Char, он не явный. Все зависит от компилятора.  Для переносимости кода рекомендуется явно указывать знаковость. 
```

Отдельно про [[Типы данных С]]

Разобрался с Float - 
1 бит под знак, 8 под экспоненту и 23 по мантиссу 
Мантисс - цифры знака. Экспонента указывает куда ставить точку относительно единицы. Т.е. 1 экспонента 0, 10, экспонента 1, 0.1 экспонента -1

[[Переменные]] и есть [[Константы и литералы]]

Структура программы
 ![[Pasted image 20240727225843.png]]
### Функция printf
технически это функция, но фактически команда 
синтаксис - printf("%d",20);  printf("формат строка", данные для вывода); 

У функции printf есть один обязательный параметр – строка, заключенная в двойные кавычки. Эту строку еще называют формат-строкой.

Напоминаю, что параметрами называется то, что мы записываем рядом с именем функции в круглых скобках.

Кроме обязательной строки форматирования есть и необязательные параметры. Они пишутся через запятую после формат-строки.

 Формат-строка.

Любой символ в формат-строке относится к одной из следующих групп:

- символы, которые выводятся на экран без изменений
- escape-последовательности
- спецификаторы формата
![[Pasted image 20240408145448.png]]

Спецификаторы формата для printf 
```
1. `%d` - для вывода целых чисел в десятичной системе.
2. `%f` - для вывода чисел с плавающей точкой (действительных чисел).
3. `%c` - для вывода символов.
4. `%s` - для вывода строк (массивов символов).
5. `%x`, `%X` - для вывода целых чисел в шестнадцатеричной системе. `%x` выводит буквы нижнего регистра, а `%X` - в верхнем.
6. `%o` - для вывода целых чисел в восьмеричной системе.
7. `%u` - для вывода беззнаковых целых чисел.
8. `%e`, `%E` - для вывода чисел в экспоненциальной форме (научной нотации). `%e` выводит экспоненту в нижнем регистре, а `%E` - в верхнем.
9. `%g`, `%G` - для вывода чисел в экспоненциальной форме или обычной десятичной форме в зависимости от значения.
10. `%%` - для вывода символа процента `%`.
```

Экранированные последовательности  (escape sequences)

1. `\n` - символ новой строки (перевод строки).
2. `\t` - символ табуляции (горизонтального пробела).
3. `\\` - обратная косая черта (сама по себе).
4. `\"` - двойная кавычка.
5. `\'` - одинарная кавычка (апостроф).
6. `\b` - символ возврата на одну позицию назад (backspace).
7. `\r` - возврат каретки (перемещение курсора в начало строки).
8. `\f` - перевод страницы (переход на новую страницу).

Дополнительные модификаторы формата
1. `%ld`, `%lu` - для вывода значений типа `long int` (длинных целых чисел) и `unsigned long int` (длинных беззнаковых целых чисел).
2. `%lld`, `%llu` - для вывода значений типа `long long int` (длинных целых чисел) и `unsigned long long int` (длинных беззнаковых целых чисел).
3. `%hd`, `%hu` - для вывода значений типа `short int` (коротких целых чисел) и `unsigned short int` (коротких беззнаковых целых чисел).
4. `%Lf` - для вывода значений типа `long double` (длинных чисел с плавающей точкой).
5. `%p` - для вывода указателей.
6. `%n` - для записи числа успешно выведенных символов в переменную типа `int*`.

1. `%[ширина]d`, `%[ширина]i`, `%[ширина]u`, `%[ширина]o`, `%[ширина]x`, `%[ширина]X`, `%[ширина]f`, `%[ширина]e`, `%[ширина]E`, `%[ширина]g`, `%[ширина]G`, `%[ширина]s` - Устанавливает минимальную ширину поля вывода. Если выводимое значение меньше заданной ширины, то оно дополняется пробелами слева до указанной ширины. Если выводимое значение больше заданной ширины, то оно выводится без изменений.
2. `%-[ширина]d`, `%-[ширина]i`, `%-[ширина]u`, `%-[ширина]o`, `%-[ширина]x`, `%-[ширина]X`, `%-[ширина]f`, `%-[ширина]e`, `%-[ширина]E`, `%-[ширина]g`, `%-[ширина]G`, `%-[ширина]s` - Левое выравнивание. Если выводимое значение меньше заданной ширины, то оно дополняется пробелами справа до указанной ширины. Если выводимое значение больше заданной ширины, то оно выводится без изменений.
3. `%+[ширина]d`, `%+[ширина]i` - Выводить знак "+" или "-" для положительных или отрицательных чисел.
4. `%0[ширина]d`, `%0[ширина]i`, `%0[ширина]u`, `%0[ширина]o`, `%0[ширина]x`, `%0[ширина]X` - Заполнение пустых мест в ширине указанным символом (обычно нулем), если выводимое значение меньше заданной ширины.

# Функция scanf


[[Консоль Git Bash]]

Некоторые математические функции

fabs(x) модуль числа x  
sqrt(x) квадратный корень из числа x  
sin(x) синус числа x (х в радианах)  
cos(x) косинус числа x (х в радианах)  
pow(x, y) вычисление xy  
exp(x) вычисление ex  
log(x) натуральный логарифм числа x  
log10(x) десятичный логарифм числа x
