# Создание класса

После сохранения формы становится доступно боковое меню, состоящее из основных объектов управления приложением:

![shema](/tutorial/images/new_app.png)

Основным объектом управления приложения является класс. Для создания класса модели данных нужно перейти в пункт меню «Classes» и в рабочей панели выбрать действие «+Class», после чего откроется форма заполнения свойств нового класса. В ней необходимо указать системное и логическое имя, а также заполнить остальные свойства атрибутов, при необходимости. Создаем класс «Tickets»:

![shema](/tutorial/images/create_app.png)

При создании класса автоматически привязывается ключевой атрибут «ID», который является уникальным идентификатором для класса. Созданный класс Tickets отображается в виде таблицы сущности в рабочей области студии:

![shema](/tutorial/images/new_class.png)

## Создание атрибута класса

Далее выбираем действие «+Attribute» для класса «Tickets», открывается форма создания атрибута Number, на ней заполняем данные о системном, логическом наименовании атрибута класса, задаем тип атрибута и указываем свойства уникальности, индексацию для поиска и запрет на пустое значение атрибута, так как атрибут «номер билета» будет являться ключевым атрибутом для данного класса:

![shema]![shema](/tutorial/images/create_attr.png) ![shema](/tutorial/images/create_attr2.png)

Аналогичным образом создаются остальные необходимые атрибуты класса. В результате для класса Tickets определен следующий атрибутивный состав:

![shema](/tutorial/images/new_attr_in_class.png)

## Редактирование свойств класса

После определения атрибутивного состава класса есть возможность добавления дополнительных свойств для класса. Например, можно добавить значение в свойство "creatorTracker" (метка пользователя, создавшего объект), уникальный составной индекс объектов класса и значение семантики класса. Для этого необходимо открыть форму класса на редактирование. Выполнить данное действие можно несколькими способами:
* Кликнув двойным щелчком по таблице класса на наименовании класса в рабочей области.
* Кликнув двойным щелчком по наименованию класса, расположенному в пункте Classes на боковой панели.
* При наличии выделенного класса в рабочей области, либо на боковой панели доступно действие Редактирования класса:

![shema](/tutorial/images/edit_class.png)

При открытии формы редактирования любым из вышеперечисленных способов в нижней части  формы доступно действие открытия класса в редакторе:

![shema](/tutorial/images/edit_json.png)

При выборе действия открывается окно, где класс отображается как файл в формате . json:

![shema](/tutorial/images/code_editor.png) (/tutorial/images/code_editor_doc.png)

Данное действие доступно на всех формах созданных объектов при редактировании. 

## Наследование
Студия позволяет применять механизм наследования для сущностей приложения. Для начала создаем базовый класс «Person» и наполняем его необходимым атрибутивным составом:

![shema](/tutorial/images/attr_person.png)

Далее создаем класс «Recipient» для которого необходимо будет наследовать атрибутивный состав класса «Person» и помимо этого, дополняем его собственными атрибутами:

![shema](/tutorial/images/attr_recipient.png)

Открываем на редактирование форму класса «Recipient» и для свойства «Ancestor» выбираем из списка значение – класс «Person»:

![shema](/tutorial/images/ancentor_recipient.png)

Таким образом, при формировании форм представления для класса «Recipient» можно заимвствовать атрибуты базового класса.

## Связи между сущностями
Функционал студии позволяет создавать связи между созданными объектами при помощи указания соответствующего типа для атрибута класса. Разберем на примере атрибута «Tickets» класса «Recipient». Открываем форму редактирования атрибута и для свойства «Type» выбираем из списка значение «Collection».  Так же необходимо указать значение класса, на который будет ссылаться коллекция для свойства «Item class»:

![shema](/tutorial/images/item_class.png)

Таким образом, на форме объекта класса «Recipient» будет отображаться коллекция объектов «Tickets». Вот как это будет выглядеть в системе:

![shema](/tutorial/images/collection_form.png)

## Построение схемы модели данных 

По тому же сценарию создаем класс «Documents» и задаем для него атрибутивный состав. После необходимо определить типы атрибутов и проставить для них ссылки на соответствующие классы.
* В классе «Recipient» открываем на редактирование атрибут «Passport» выбираем тип – «Collection» и в поле «Item class» выбираем из списка класс «Documents»:

![shema](/tutorial/images/item_class_doc.png)

* В классе «Tickets» открываем на редактирование атрибут «Recipient» выбираем тип – «Reference» и в поле «Reference class» выбираем из списка класс «Recipient»:

![shema](/tutorial/images/ref_class_recipient.png)

* В классе «Documents» открываем на редактирование атрибут «Recipient» выбираем тип – «Reference» и в поле «Reference class» выбираем из списка класс «Recipient».
В итоге получаем схему приложения «Social nutrition tickets» следующего вида:

![shema](/tutorial/images/shems_workflow.png)

## Формула для расчета количества льготных категорий получателя
Теперь нам необходимо задать формулу для автоматического расчёта количества льготных категорий у одного получателя талона. Способ выбора льготной категории на форме задан при помощи атрибутов с типом «Boolean». Для обозначения льготной категории получателя необходимо обозначить положительное значение чек-бокса для соответственных атрибутов:

![shema](/tutorial/images/category_form.png)

После сохранения формы для атрибута «Number of selected categories» будет рассчитано значение равное количеству льготных категорий получателя талона.
Формула рассчета: преобразуем значение логического атрибута в число – где 1 - это true, а false – это 0 и суммируем полученные значения. Таким образом, получаем количество выбранных категорий получателя: 

![shema](/tutorial/images/formula_category.png)

## Формула расчета максимально допустимой суммы использования талона
Для формы талона зададим формулу автоматического расчёта максимально допустимой суммы использования талона, которая зависит от количества льготных категорий у пользователя.   
В классе «Tickets» открываем форму редактирования атрибута «Maximum allowable amount of use» и задаем значение для свойства «Formula» следующего вида:

![shema](/tutorial/images/formula_sum.png)

То есть умножаем значение количества категорий получателя на максимальную сумму рассчитанную на одну льготную категорию (в данном случае 200).

## Ограничение на создание объектов в коллекцию
Гражданин получает талоны из расчета 1 талона на неделю  каждые 4 недели необходимо обратиться в соц. защиту, где оператор создает на форме получателя в коллекцию «Tickets» только 4 талона. При наличии в коллекции 4-ех действующих талонов, действие «Создать» блокируется для коллекции. Для этого на форме представления атрибута «Tickets» для свойства «Availability» необходимо задать значение следующего вида *«.tickets.length < 4»* тем самым ограничивая количество текущих объектов в коллекции.

## Формула расчета даты завершения талона
Так же для формы талона зададим автоматический расчет даты завершения срока действия талона исходя из расчета что максимальный срок на использование билета составляет 28 дней (4 недели). Для атрибута «Date of completion» класса «Tickets» в свойстве «Formula» задаем значение следующего вида:

![shema](/tutorial/images/formula_date_end.png)

В которой выполнено действие добавления к дате выдачи билета 28 дней.

### Следующая страница: [Создание навигации](/tutorial/ru/3_create_navigation.md)  

--------------------------------------------------------------------------  

 #### [Licence](/LICENSE) &ensp;  [Contact us](https://iondv.ru/index.html) &ensp;  [English](/tutorial/en/2_create_class.md)    &ensp;   <div><img src="https://mc.iondv.com/watch/local/docs/framework" style="position:absolute; left:-9999px;" height=1 width=1 alt="iondv metrics"></div>        
--------------------------------------------------------------------------  

Copyright (c) 2018 **LLC "ION DV"**.  
All rights reserved.  