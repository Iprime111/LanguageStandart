# Стандарт файла абстрактного синтаксического дерева
## Базовые сведения
Дерево сохраняется в файл в **текстовом** формате. Для сохранения каждого из узлов дерева используется запись вида:

```
( nodeType nodeContent leftChild rightChild )
```

Если `leftChild` или `rightChild` - непустое поддерево, то его запись аналогична представленной выше. Если же потомка у узла нет, то ставится символ подчеркивания, отделенный пробелами с двух сторон.

> [!IMPORTANT]
> Каждый из элементов записи дерева должен быть отделен от соседних **одним** пробелом. Пробела в начале быть **не должно**.

> [!IMPORTANT]
> В случае, если узел не хранит никаких данных, помимо своего типа, его формат становится `( nodeType leftChild rightChild ) `

### Пример дерева
```
( 1 31 ( 2 71 _ ( 3 18 _ _ ) ) _ )
```
Данная запись соответствует дереву на картинке ниже:

~Исправить пример и вставить картинку~

## Типы узлов
Первым параметром в каждом из узлов является число, отвечающее за его тип. Список типов и их содержимого представлен в таблице:

| Номер типа | Тип узла             | Содержание узла                                                                  |
|------------|----------------------|----------------------------------------------------------------------------------|
| 1          | `Constant`           | Число в виде десятичной дроби                                                    |
| 2          | `Identifier`         | Строка, ограниченная кавычками и содержащая идентификатор переменной или функции |
| 3          | `Keyword`            | Номер ключевого слова                                                            |
| 4          | `FunctionDefinition` | Идентификатор функции, задаваемой данным узлом                                   |
| 5          | `Parameters`         | Нет хранимой величины                                                            |
| 6          | `VarDeclaration`     | Идентификатор создаваемой переменной                                             |
| 7          | `Call`               | Нет хранимой величины                                                            |

Рассмотрим подробнее каждый из типов узлов:

### Constant
Данный тип задает константу времени компиляции, в программе выглядящую, как `1.543` или `-5.67`. Не может иметь потомков и всегда является листом дерева.

Пример:
```
( 1 -1.543 _ _ )
```

### Identifier
Задает идентификатор переменной (или функции) и является строкой (возможно состоящей из нескольких слов). Также, как и константа не может иметь потомков и является листом дерева.

Пример:
```
( 2 "foo bar" _ _ )
```

### Keyword
Узел данного типа является ключевым словом, таким как операторы `return`, `if` или имя типа `Number`. Список всех ключевых слов, реализация которых предусмотрена стандартом представлен ниже. Ключевое слово задается его индексом.

Пример:

```
( 3 24 ( 1 -7 ) ( 2 "sum" ) )
```

### FunctionDefinition
Задает объявление новой функции и содержит ее идентификатор. В левой ветке содержит тип возвращаемого значения функции, а в правой ноду типа `Parameters`

Пример:
```
( 4 "foo" ( 3 51 _ _ ) ( 5 ... ) )
```

### Parameters
Данный узел не содержит в себе никаких данных, за исключением типа. В левой ветке узла находится список параметров объявляемой функции, а в правой - тело функции.

> [!IMPORTANT]
> Важно, что тело функции должно начинаться с ~точки с запятой~ оператора последовательного исполнения


Пример:

~Написать пример~

### VarDeclaration

Обозначает создание новой переменной (в текущей области видимости). Содержит имя новой переменной. Левый потомок - тип новой переменной, правый потомок - идентификатор переменной, либо выражение ее инициализации (выражение присваивания).

Пример:

```
( 6 "foo" ( 3 51 _ _ ) ( 2 "foo" ) )
```

### Call

Задает вызов функции. Не содержит в себе никаких данных, кроме типа. В левой ветке содержит список параметров функции, а в правой ее идентификатор.

Пример:
```
( 7 ( ... ) ( 2 "foo" ) )
```

## Список ключевых слов

|Номер|Ключевое слово|Описание|
|-----|--------------|--------|
|11|if       |Условный оператор|
|12|while    |Оператор цикла|
|13|=        |Оператор присваивания|
|21|sin      |Синус |
|22|cos      |Косинус|
|23|floor    |Округление вниз|
|24|+        |Сложение|
|25|-        |Вычитание|
|26|*        |Умножение|
|27|/        |Деление|
|28|diff     |Оператор дифференцирования|
|29|sqrt     |Квадратный корень|
|31|==       |Равенство|
|32|<        |Меньше|
|33|>        |Больше|
|34|<=       |Меньше или равно|
|35|>=       |Больше или равно|
|36|!=       |Не равно|
|37|&&       |Логическое И|
|38|\|\|     |Логическое ИЛИ|
|39|!        |Отрицание|
|41|;        |Оператор последовательного исполнения|
|42|,        |Оператор перечисления|
|51|number   |Число с плавающей точкой|
|61|in       |Оператор ввода|
|62|out      |Оператор вывода|
|71|return   |Оператор возврата|
|72|break    |Оператор выхода из цикла|
|73|continue |Оператор перехода на следующую итерацию|
|74|abort    |Оператор завершения программы

## Оператор посдеовательного исполнения

Отделяет между собой ноды c функциями, строками(операторами/операциями). Пример такого дерева:
```
( 3 41 ( 3 13 ( 15 ) ( 2 "var" ) ) ( 3 41 ( ... ) ( 3 41 ( ... ) ( .. )) ) )
```
~Макс, если хуйню написал в плане терминов, подредачь~.

## Арифметические выражения

~Написать~

## Выражения присваивания

~Написать~

## Условные и циклические операторы

~Написать~

## Задание параметров функции

~Написать~

## Оператор возврата значения

~Написать~
