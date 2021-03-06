# if

### Сниппет выводит информации по условию

#### Как работает?

Если при вызове `if` условие в параметре `is` выполняется, то выведется содержимое параметра `then`, если нет - содержимое параметра `else`.

Если необходимо ничего не выводить через `then` или `else`, то можно вовсе не задавать этот параметр.

#### Некэшируемый вызов

При работы с внешними плейсхолдерами необходимо вызывать сниппет некешируемым.

А внешний плейсхолдер это, например, `[+pages+]` из **Ditto**.

#### Пример вызова

```
// пример вызова кэшируемого...
[[if? &is=`[*parent*]:=:5` &then=`true` &else=`false`]]

// и некэшируемого if
[!if? &is=`[*parent*]:=:5` &then=`true` &else=`false`!]
```


### Параметры сниппета

Параметр|Описание|Возможные значения|По-умолчанию
--------|--------|------------------|------------
**is**|Обрабатываемое условие|что сравниваем:как сравниваем:с чем сравниваем|Пусто
**then**|Содержимое для вывода, если условие верно|`@tpl:chunkname` или любой html-код с тегами MODX|Пусто
**else**|Содержимое для вывода, если условие не верно|`@tpl:chunkname` или любой html-код с тегами MODX|Пусто
**math**|Включает выполнение математических функций в параметре `is`|on|Пусто
**separator**|Разделитель в условии|Например, `~`| `:` 

Для того чтобы парсер не обрабатывал вариант и `then` и `else`, как это делает **PHx**, вызывайте: `&then='@TPL:chunkname'` — где `chunkname` - имя чанка.

В этом случае будет выполнен только результирующий чанк.

***

### Операторы используемые в условии

**is, =** - равно

**not, !=** - не равно

**>, gt** - больше

**<, lt** - меньше

**>=, gte** - больше или равно

**lte, <=** - меньше или равно

**isempty, empty** - проверка на пустоту

**not_empty, !empty** - проверка на заполненность

**null, is_null** - проверка, является ли значение переменной равным NULL

**in_array, inarray, in** - наличие в массиве

**not_in, !in** - отсутствие в массиве

***

### Выполнение математических функций:

	is=`[+id+]*10:=:30`


### Примеры использования

	1) Выводить акцию нужно только в каталоге с ID = 5
	[[if? &is=`[*parent*]:=:5` &then=`@TPL:akcia`]]

	2) Выводить акцию нужно только в каталоге с ID = 5 или в каталоге с шаблоном №7,8,9
	[[if? &is=`[*parent*]:=:5:or:[*template*]:in:7,8,9` &then=`@TPL:akcia`]]

	3) Выводить акцию нужно только в каталоге с ID = 5 и только в ресурсе с шаблоном №2
	[[if? &is=`[*parent*]:=:5:and:[*template*]:=:2` &then=`@TPL:akcia`]]

	4) Выводить акцию нужно только в каталоге с ID = 5 и только в ресурсе с шаблоном №2 или в других шаблонах но с ТВ show_akcia = 1
	[[if? &is=`[*parent*]:=:5:and:[*template*]:=:2:or:[*show_akcia*]:=1` &then=`@TPL:akcia`]]

	5) Выводить акцию только для товаров с ценой в диапазоне >300$ <=700$
	[[if? &is=`[*price*]:>:300:and:[*price*]:<=:700` &then=`@TPL:akcia`]]

	6) Выводить при кратности записи Ditto 3
	[[if? &is=`[+ditto_iteration+]+1:%:3` &then=`true` &else=`false`]]
	[[if? &is=`[+ditto_index+]+1:%:3` &then=`true` &else=`false`]]

	7) Выводить при кратности записи Ditto 3 но с умножением значения
	[[if? &is=`[+ditto_iteration+]*2:%:3` &then=`true` &else=`false` &math=`on`]]

	8) Выводить значение математического выражения
	[[if? &is=`[+ditto_iteration+]*2` &math=`on`]]
