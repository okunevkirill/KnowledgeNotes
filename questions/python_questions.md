# Вопросы по Python

_Примечание_ - *общие вопросы по ООП и по встроенным пакетам находятся отдельно.*

___

<details> 
<summary><strong>Что такое Python?</strong></summary>

Python - высокоуровневый интерпретируемый язык программирования с
неявной, но строгой, динамической типизацией.

> - Понятие `динамическая типизация` означает что тип переменной задаётся
    в момент присваивания значения (*может быть изменён в коде позже*).
> - Понятие `строгая типизация` означает что нет неявных преобразований от одного
    типа в другой (*нельзя неявно преобразовать число в строку*).
> - Понятие `неявная типизация` означает что нет необходимости указывать
    типы, — "Если что-то выглядит как утка, плавает как утка и крякает как
    утка, это наверняка и есть утка." (*корректность использования объекта определяется его методами*)

</details>

<details>
<summary><strong>Что значит интерпретируемый язык и в чем разница от компилируемого?</strong></summary>

Интерпретируемый язык - язык, в котором инструкции не исполняются целевой машиной,
а считываются и исполняются другой программой (*пошагово выполнение команд для машины*).

Компилируемый язык — язык, в котором программа, будучи скомпилированной,
содержит инструкции целевой машины (*за один подход формируется все команды для машины*).

> Наиболее распространённая версия интерпретатора (CPython) является
> интерпретатором компилирующего типа, — компилятор переводит исходный код
> программы в промежуточное представление (байт-код),
> а интерпретатор (виртуальная машина) выполняет этот байт-код.

</details>

<details>
<summary><strong>Какие типы данных есть в Python?</strong></summary>

В Python есть следующие основные встроенные типы данных:

- None
- числа (`int`, `float`, `complex`)
- строки (`str`)
- логические (`bool`)
- списки (`list`)
- словари (`dict`)
- кортежи (`tuple`)
- множества (`set`)
- байты (`bytes`)
- массивы байт (`bytearray`)
- статичное множество (`frozenset`)

Эти типы данных можно, в свою очередь, классифицировать по нескольким признакам:

- изменяемые (списки, словари, множества, bytearray)
- неизменяемые (числа, строки, кортежи и frozenset)
- упорядоченные (списки, кортежи, строки и с версии 3.6 словари)
- неупорядоченные (множества, frozenset)

</details>

<details>
<summary>
  <strong>В чём принципиальная разница между списком и словарём?</strong>
</summary>

Несмотря на то, что и список и словарь являются коллекциями, между ними
довольно много различий. Ключевым отличием является способ организации работы с
данными:

- В списке работа с данными производится по
  индексу (*почти как массив, но типы могут отличаться*).
- В словаре работа с данными производиться по
  ключу (*словарь представляет собой реализацию хеш-таблицы и является хранилищем ключей*).

Исходя из способа работы данных вытекает разница в сложности при работе
с данными в словаре и в списке.

| Тип данных | Вставка | Получение | Поиск | Удаление |
|------------|:-------:|:---------:|:-----:|:--------:|
| список     |  O(n)   |   O(1)    | O(n)  |   O(n)   |
| словарь    |  O(1)   |   O(1)    | O(1)  |   O(1)   |

</details>

<details>
<summary><strong>Что такое сложность алгоритма?</strong></summary>

Сложность алгоритма - это количественная оценка ресурсов, затрачиваемых при
использовании данного алгоритма.
Зачастую пот данным понятием понимают вычислительную сложность (сколько времени,
либо какой объём памяти потребуется для выполнения алгоритма).
Когда говорят об анализе сложности алгоритма, обычно подразумевают то,
насколько быстро он работает (*рассматривают работу с данными стремящимися к бесконечности*).
Сложность обозначают буквой `O` (*о большое*).

</details>

<details>
<summary><strong>Что такое функции и зачем они нужны?</strong></summary>

Функция - фрагмент программного кода, к которому можно обратиться
из другого места программы.

Функции используют:

- для уменьшения повторяемости кода;
- процедурной декомпозиции (*распределение кода на части с чёткими задачами*).

</details>

<details>
<summary><strong>Как в CPython управляется память?</strong></summary>

Управление памятью – это процесс эффективного распределения, выделения и координации памяти.

В CPython распределение и освобождение памяти выполняется автоматически,
с помощью подсчета ссылок. Это означает, что диспетчер памяти отслеживает
количество ссылок на каждый объект в программе. Когда счетчик ссылок объекта
падает до нуля, что означает, что объект больше не используется, сборщик
мусора (*часть диспетчера памяти*) автоматически освобождает память от этого
конкретного объекта. Счетчик ссылок увеличивается, если объекту присваивается
новое имя или он помещается в контейнер, такой как кортеж или словарь.
Аналогично, счетчик ссылок уменьшается, когда ссылка на
объект переназначается, когда ссылка на объект выходит из области видимости или
когда объект удаляется.

Память представляет собой кучу, которая содержит объекты и другие структуры данных,
используемые в программе. Выделение и перераспределение этого пространства кучи
контролируется менеджером памяти Python.

Алгоритм подсчета ссылок очень простой и эффективный, но у него есть один
большой недостаток. Он не умеет определять циклические ссылки.
Именно из-за этого, в питоне существует дополнительный сборщик, именуемый
Garbage Collector (GC), который следит за объектами с потенциальными
циклическими ссылками. В Python, алгоритм подсчета ссылок является
фундаментальным и не может отключен, тогда как GC опционален
и может быть отключен.

> Циклические ссылки происходят когда один или более объектов ссылаются друг на друга.

_Пример создания циклической ссылки:_

```pycon
obj = []
obj.append(obj)
```

</details>

<details>
<summary><strong>Что такое итератор?</strong></summary>

Итератор - поведенческий паттерн, позволяющий последовательно обходить
сложную коллекцию, без раскрытия деталей её реализации.

Простыми словами итератор — это штука, описывающая в себе правило
по которому перебирается содержимое той или иной "коробки".
С точки зрения Python - это любой объект, у которого есть метод `__next__`.
Этот метод возвращает следующий элемент, если он есть, или возвращает
исключение `StopIteration`, когда элементы закончились.
В Python принято, что у каждого итератора присутствует метод
`__iter__` - то есть, любой итератор является итерируемым объектом.

> Для полной реализации протокола итератора требуется определить методы
> `__next__` и `__iter__`.

</details>

<details>
<summary>
  <strong>В чём разница между итератором и итерируемым объектом?</strong>
</summary>

Итерируемый объект - объект, реализующий метод `__iter__` или
`__getitem__` (*объект элементы которого можно пересчитать*).
Для итератора строга обязательно реализация метода
`__next__` (*обеспечивает выдачу очередного элемента итерируемого объекта*).

</details>

<details>
<summary><strong>Что такое генератор?</strong></summary>

Генератор в Python — это языковая конструкция, которую можно реализовать
двумя способами: как функция с ключевым словом `yield` или как генераторное выражение.
В результате вызова функции или вычисления выражения, получаем объект-генератор
типа `GeneratorType`. Генераторы можно считать подвидом итераторов, а способ
их создания – инструментом для создания несложных итераторов.

</details>

<details>
<summary><strong>Что такое декоратор?</strong></summary>

Декоратор - структурный паттерн, позволяющий изменяет поведение одного объекта другим.

> Декоратором может быть любой вызываемый объект: функция, лямбда, класс, экземпляр класса.

</details>

<details>
<summary><strong>Что такое контекстный менеджер?</strong></summary>

Менеджеры контекста (`with`) - объект позволяющий выделять и освобождать ресурсы строго
по необходимости. В Python события входа и выхода определяются методами
`__enter__` и `__exit__`.

`__enter__` срабатывает в тот момент, когда ход исполнения программы переходит внутрь `with`.

`__exit__` срабатывает в момент выхода из блока, в том числе и по причине исключения.

> Самый распространённый контекстный менеджер – класс, порожденный функцией `open`.
> Он гарантирует, что файл будет закрыт даже в том случае, если внутри блока возникнет ошибка.

</details>

<details>
<summary><strong>Что значит *args, **kwargs? И зачем нам их использовать?</strong></summary>

Выражения `*args` и `**kwargs` объявляют в сигнатуре функции.
Они означают, что внутри функции будут доступны переменные с именами
`args` и `kwargs` (*без звездочек*). Можно использовать другие имена,
но это считается дурным тоном.

- `args` – это кортеж, который накапливает позиционные аргументы.
- `kwargs` – словарь именованных аргументов, где ключ – имя параметра,
  значение – значение параметра.

> Если в функцию не передано никаких параметров, переменные будут
> соответственно равны пустому кортежу и пустому словарю, а не `None`.

</details>

<details>
<summary><strong>Что такое dunder методы, для чего нужны?</strong></summary>

Dunder методами (*магическими методами*) называют методы, имена которых
начинаются и заканчиваются двойным подчеркиванием.

_Примеры_:

- `__init__`: инициализатор класса
- `__add__`: сложение с другим объектом
- `__eq__`: проверка на равенство с другим объектом
- `__iter__`: возвращает итератор

> Метод `__init__` именно инициализатор, — *НЕЛЬЗЯ* его именовать конструктором.

</details>

<details>
<summary><strong>Для чего предназначен модуль __init__.py?</strong></summary>

Модуль `__init__.py` - специальный модуль "подсказывающий" интерпретатору Python,
что каталог следует воспринимать именно как пакет.

> В простейшем случае `__init__.py` может быть просто пустым файлом, но он
> также может выполнять код инициализации для пакета или устанавливать
> переменную `__all__`.
</details>