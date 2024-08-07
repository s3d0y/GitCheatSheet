
Чтобы понять чему равны значения переменных, нужно знать **когда** в `x` записывается новое значение.

```cpp
int x, y;
x = 2;
y = x++ + x++;
```

В языке Си есть понятие **sequence point** [точка следования](https://ru.wikipedia.org/wiki/%D0%A2%D0%BE%D1%87%D0%BA%D0%B0_%D1%81%D0%BB%D0%B5%D0%B4%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D1%8F) - точка программы, в которой гарантируется, что все побочные эффекты предыдущих вычислений уже проявились, а побочные эффекты последующих ещё отсутствуют.

Для операторов `++` и `--` такой точкой будут операторы `;` и `,` (вычисляет значение слева, _потом_ вычисляет значение справа, например `x = 5, y = 3;`)

Скобки не являются такой точкой. То есть в `x++ + x++;` в `x` запишут изменения гарантированно к `;`, но могут записать и раньше. Так что никто не гарантирует, что в первом `x++` к вычислению второго `x++` значение `x` **уже изменилось**. И никто не гарантирует, что значение ещё **не изменилось**.

_Не `x`, а кот Шредингера. То ли 5, то ли 6._

В языке Си ввели понятие **неопределенное поведение** (undefined behaviour). `x++ + x++` - пример такой неопределенности.

- Выражение с undefined behaviour может иметь **любое значение**. То есть тут `x++ + x++` по стандарту может быть хоть 11, хоть 10, хоть -734. Все значения с точки зрения стандарта равнозначны.
    
- Если часть выражения имеет undefined behaviour, то все выражение тоже имеет undefined behaviour. То есть и `x` у нас может быть 6, 7 или -123.
    

Если в выражении переменная изменяется более одного раза, то результат выражения не определен (undefined behaviour).

**Деление на 0 - тоже undefined behaviour.**

Хорошая практика: если над вашим выражением надо думать, как над синтаксической головоломкой, упростите его. Это поможет повысить читаемость кода и избежать undefined behaviour.