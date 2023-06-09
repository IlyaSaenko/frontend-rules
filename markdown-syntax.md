## Вся информация взята с этого [сайта](https://doka.guide/tools/markdown/)

Для экранирования служебных символов Markdown 
нужно поставить обратную косую черту перед каждым из них
(\*, \_, \*\*).

## Заголовки
# Заголовок 1 уровня
## Заголовок 2 уровня
### Заголовок 3 уровня
#### Заголовок 4 уровня
##### Заголовок 5 уровня
###### Заголовок 6 уровня

# Параграф
Подряд идущие строчки будут склеены в одну, если не добавить жёсткий перенос.<br>Существует несколько способов, как это можно сделать:

- добавить два (или больше) пробелов в конце строки <пробел><пробел>;
- добавить обратную косую черту в конце строки (один обратный слеш \\);
- добавить HTML-тег переноса строки <br>

# Выделение текста

Обычный текст

*Курсивный текст*<br>
_Другой курсивный текст_

**Жирный текст**<br>
__Другой жирный текст__

***Оба стиля***<br>
___Оба стиля___<br>

Зачеркивание
~~Привет, Вова!~~\


# Подчёркивания (Setext-style)
Секция статьи "Подчёркивания (Setext-style)"
«Подчёркивание» параграфа знаками равно (=) или дефисами (-) делает его заголовком первого или второго уровня соответственно. Уровень заголовка зависит только от типа «чёрточек», их количество значения не имеет.

Между текстом и «подчёркиванием» не должно быть пустых строк.

Заголовок 1 уровня
==================

Заголовок 2 уровня
------------------

Заголовок, который подчеркнули одним символом
-

Заголовок второго
уровня из нескольких
строчек текста
------------------

# Списки

- Помидор
+ Бублик
* Молоко

1. Хлеб
2. Молоко
3. Помидоры

__если ставить одно число номера будут идти по порядку__
1. Хлеб
1. Молоко
1. Помидоры

# Вложенность

+ Хлеб
+ Молочные продукты
    1. Кефир
    2. Ряженка

1. Молоко
2. Хлебобулочные изделия
    + Бублик
    + Ватрушка

#Цитаты
> Одна треугольная скобка
превращает в цитату несколько строк,
идущих друг за другом.

> # Цитаты великих людей
> Ваша работа заполнит большую часть жизни и единственный способ быть
> полностью довольным — делать то, что по-вашему является великим делом.
> И единственный способ делать великие дела — любить то, что вы делаете.
>
> *— Стив Джобс, Речь в Стенфорде*

> Первая, родительская цитата
> > А это уже вторая,\
> > дочерняя цитата

# Исходный код
Секция статьи "Исходный код"
Markdown позволяет специальным образом размечать исходный код, все символы внутри будут автоматически экранированы. Есть 3 способа, как это можно сделать:

Обернуть код одной-двумя парами бэктиков (`код`)
Обернуть код тремя и более парами бэктиков (```код```)
Поставить таб или 4 пробела перед каждой строчкой кода

Функция `alert()`
вызывает диалоговое окно.

Сумму двух переменных
можно вывести так:
``const a = 1
const b = 2
alert(a + b)``

После обозначения языка программирования визуально ничего не изменится, 
но это даст возможность дополнительным плагинам и скриптам подсветить код внутри блока.
```javascript
const a = 1
const b = 2

console.log(a + b)
```
Отступ
Секция статьи "Отступ"
Другой способ выделить код — поставить перед ним таб или 4 пробела.
Исходный код необходимо отделять пустой строкой от предыдущего блока.

Метод ```.toString()```
превращает числа в строку.

Его можно использовать так:

    const a = 1
    const b = 2

    (a + b).toString()

Ссылки
Секция статьи "Ссылки"
Markdown предлагает 3 стиля разметки ссылок: строчный, справочный и автоматический.

### Строчные

Для вставки ссылки в строчном стиле необходимо воспользоваться следующей конструкцией:
[Текст ссылки](URL). Есть возможность добавить подсказку, для этого нужно после URL дописать текст в кавычках: [Текст ссылки](URL "Подсказка").

Привет, [Дока](https://doka.guide "Энциклопедия про web-dev")!

### Справочные

Для вставки ссылки в справочном стиле нужно написать [Текст ссылки][Ключ] в том месте,
где вы хотите её поместить, а где-нибудь выше или ниже добавить сноску [Ключ]: URL "Подсказка"

У [Доки][1] есть свой [репозиторий][repo].


[1]: https://doka.guide "Энциклопедия про web-dev"
[repo]: https://github.com/doka-guide "Репозиторий Доки"

### Автоматические

Markdown позволяет использовать упрощённый вариант для вставки ссылок,
для этого нужно просто обернуть URI треугольными скобками (<URI>).

Можно вставлять адреса электронной почты (<hi@doka.guide>), 
тогда мы автоматически получим ссылку типа mailto:.

Заходите на <https://doka.guide>
или присылайте нам письма на <hi@doka.guide>

# Изображения
Конструкции для вставки изображений очень похожи на те, что используются для ссылок. 
Предлагается 2 стиля разметки: строчный и справочный.

### Строчные
Для вставки изображения в строчном стиле необходимо воспользоваться конструкцией ![Alt текст]​(URL картинки). При желании можно добавить подсказку: ![Alt текст](URL картинки "Подсказка").

![Одна собака](dog.png "Собака смотрит влево")

### Справочные
Для вставки изображения в справочном стиле нужно написать ![Alt текст][Ключ] в том месте,
где вы хотите его поместить, а где-нибудь выше или ниже описать картинку по ключу [Ключ]: URL картинки "Подсказка".

![Одна собака][1]

[1]: dog.png "Собака смотрит влево"

# Горизонтальный разделитель
Для разделения смысловых блоков можно использовать горизонтальную черту (<hr>).
Чтобы это сделать, необходимо поставить на одной строке три (или более) дефиса (-),
подчёркивания (_) или звёздочки (*). Они не обязательно должны идти друг за другом,
между ними могут быть табы или пробелы.

---

***

_	_	_

*  * *  *

------------

# Таблицы

Колонки таблицы размечаются с помощью вертикальных черт (|),
а заголовок отделяется дефисами (-).

| Место | Участник | Рейтинг |
|-------|----------|---------|
| 1     | Саша     | 118     |
| 2     | Юля      | 92      |
| 3     | Даниил   | 36      |

Можно поставить двоеточие (:) рядом с дефисами для выравнивания текста:

по левой стороне (|:----|)
по центру (|:----:|)
по правой стороне (|----:|)

| Место | Участник | Рейтинг |
|------:|:--------:|:--------|
| 1     | Саша     | 118     |
| 2     | Юля      | 92      |
| 3     | Даниил   | 36      |

Ячейки таблицы могут не соответствовать друг другу по размеру.
(Идея просто не умеет отображать)

|Место|Участник|Рейтинг|
|---:|:---:|:---|
|1|Саша|118|
|2|Юля|92|
|3|Даниил|36|

# Список задач

Для создания списка задач используется синтаксис маркированного списка,
но с добавлением чекбоксов ([ ] или [x]) после маркеров.
- [x] Выйти на улицу
- [x] Зайти в магазин
- [ ] Купить продукты
    - [x] Молоко
    - [x] Хлеб
    - [ ] Помидоры
- [ ] Вернуться домой

# Теги
Ссылка на вопросы по определённому тегу пишется просто в квадратных скобках с префиксом tag:
Все вопросы по тегу [tag:javascript] на нашем сайте.

# Спойлер
Если после символа цитирования поставить восклицательный знак (>!), 
то цитата выведется свёрнутой, и развернуть её пользователь сможет, кликнув по ней.

В конце пятого эпизода выясняется, что
>! он его отец.

#### Еще один вариант(работающий)\

Сколько будет 2 + 2?
<details> 
  <summary>Правильный ответ</summary>
  Четыре
</details>






