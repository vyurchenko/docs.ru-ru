---
title: "Форма деревьев команд | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2215585e-ca47-45f8-98d4-8cb982f8c1d3
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Форма деревьев команд
Модуль создания кода SQL отвечает за создание кода SQL, зависящего от конкретного сервера запроса, на основе данного входного выражения дерева команд запроса.  В этом разделе описываются характеристики, свойства и структура деревьев команд запроса.  
  
## Общие сведения о деревьях команд запроса  
 Дерево команд запроса является представлением объектной модели запроса.  Деревья команд запроса используются для двух целей.  
  
-   Представление входного запроса, который задан по отношению к [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)].  
  
-   Представление выходного запроса, который передается поставщику и описывает запрос по отношению к серверу базы данных.  
  
 Деревья команд запроса поддерживают более развитую семантику по сравнению с запросами, совместимыми с SQL:1999, включая поддержку работы с вложенными коллекциями и операциями типа, такими как проверка того, имеет ли сущность конкретный тип, или фильтрации наборов с учетом типа.  
  
 Свойство DBQueryCommandTree.Query является корнем дерева выражения, которое описывает логику запроса.  Свойство DBQueryCommandTree.Parameters содержит список параметров, которые используются в запросе.  Дерево выражения состоит из объектов DbExpression.  
  
 Объект DbExpression представляет некоторое вычисление.  Для составления выражений запросов [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] предоставляет несколько видов выражений, включая константы, переменные, функции, конструкторы и стандартные реляционные операторы, такие как фильтрация и соединение.  Каждый объект DbExpression имеет свойство ResultType, которое представляет тип результата, формируемого этим выражением.  Этот тип выражается как TypeUsage.  
  
## Формы деревьев команд выходного запроса  
 Деревья команд выходного запроса подробно представляют реляционные запросы \(SQL\) и соответствуют намного более строгим правилам по сравнению с теми, которые применяются к деревьям команд запроса.  Они обычно содержат конструкции, которые легко преобразуются в код SQL.  
  
 Деревья входных команд выражаются применительно к концептуальной модели, которая поддерживает свойства навигации, ассоциации среди сущностей и наследование.  Деревья выходных команд выражаются применительно к модели хранения.  Деревья входных команд позволяют проецировать вложенные коллекции, а деревья выходных команд \- нет.  
  
 Деревья выходных команд запроса формируются с использованием подмножества доступных объектов DbExpression, и даже некоторые выражения в этом подмножестве имеют ограниченное использование.  
  
 Операции типа, такие как проверка того, имеет ли данное выражение конкретный тип, или фильтрация наборов с учетом типа, отсутствуют в деревьях выходных команд.  
  
 В деревьях выходных команд для проекций используются только выражения, которые возвращают значения типа Boolean, и только для предикатов в выражениях, требующих предиката, таких как фильтр или инструкция CASE.  
  
 Корнем деревьев выходных команд запроса является объект DbProjectExpression.  
  
### Типы выражений, не присутствующих в деревьях выходных команд запроса  
 Следующие типы выражений не допускаются в дереве выходных команд запроса и не требуют обработки поставщиками.  
  
 DbDerefExpression  
  
 DbEntityRefExpression  
  
 DbRefKeyExpression  
  
 DbIsOfExpression  
  
 DbOfTypeExpression  
  
 DbRefExpression  
  
 DbRelationshipNavigationExpression  
  
 DbTreatExpression  
  
### Ограничения выражений и примечания  
 В деревьях выходных команд запроса многие выражения могут использоваться только в ограниченном виде.  
  
#### DbFunctionExpression  
 Могут передаваться следующие типы функций:  
  
-   Канонические функции, распознаваемые в пространстве имен Edm.  
  
-   Встроенные функции \(хранилища\), которые распознаются BuiltInAttribute.  
  
-   Определяемые пользователем функции.  
  
 Канонические функции \(дополнительные сведения см. в разделе [Канонические функции](../../../../../docs/framework/data/adonet/ef/language-reference/canonical-functions.md)\) задаются как часть [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)], а поставщики должны предоставлять реализации для канонических функций на основе этих спецификаций.  Функции хранилища основаны на спецификациях из соответствующего манифеста поставщика.  Определяемые пользователем функции основаны на спецификациях из языка SSDL.  
  
 Кроме того, функции с атрибутом NiladicFunction не имеют аргументов и должны преобразовываться без круглой скобки в конце.  Иными словами, следует писать *\<functionName\>* вместо *\<functionName\>\(\)*.  
  
#### DbNewInstanceExpression  
 Выражение DbNewInstanceExpression может встречаться только в следующих двух случаях.  
  
-   Как свойство Projection объекта DbProjectExpression.  При его использовании в этом качестве виде применяются следующие ограничения.  
  
    -   Тип результата должен быть типом строки.  
  
    -   Каждый из его аргументов представляет собой выражение, которое формирует результат с примитивным типом.  Как правило, каждый аргумент является скалярным выражением, таким как PropertyExpression на основе DbVariableReferenceExpression, вызовом функции или арифметическим вычислением DbPropertyExpression на основе DbVariableReferenceExpression или вызова функции.  Однако выражение, представляющее скалярный вложенный запрос, может также встретиться в списке аргументов для выражения DbNewInstanceExpression.  Выражение, которое представляет скалярный вложенный запрос, \- это дерево выражения, которое представляет вложенный запрос, возвращающий одну единственную строку и один столбец примитивного типа с корнем объекта DbElementExpression  
  
-   С возвращаемым типом коллекции, и в этом случае он определяет новую коллекцию выражений, предоставленных как аргументы.  
  
#### DbVariableReferenceExpression  
 Выражение DbVariableReferenceExpression должно быть дочерним элементом узла DbPropertyExpression.  
  
#### DbGroupByExpression  
 Свойство Aggregates выражения DbGroupByExpression может иметь только элементы типа DbFunctionAggregate.  Никакие прочие типы агрегатов не предусмотрены.  
  
#### DbLimitExpression  
 Значением свойства Limit может быть только DbConstantExpression или DbParameterReferenceExpression.  Кроме того, начиная с версии 3.5 платформы .NET Framework, свойство WithTies всегда имеет значение false.  
  
#### DbScanExpression  
 При использовании в деревьях выходных команд выражение DbScanExpression фактически представляет просмотр по таблице, представлению или запрос хранилища, представленный с помощью EnitySetBase::Target.  
  
 Если свойство метаданных «Defining Query» цели имеет значение, отличное от null, оно представляет запрос, текст запроса для которого предусмотрен в этом свойстве метаданных на конкретном языке \(или диалекте\) поставщика, как указано в определении схемы хранилища.  
  
 В противном случае цель представляет таблицу или представление.  Его префиксом схемы находится либо в свойству метаданных «Schema», если оно не равно null. В противном случае применяется имя контейнера сущностей.  Именем таблицы или представления является либо свойство метаданных «Table», если оно не равно null. В противном случае применяется свойство Name базы набора сущностей.  
  
 Все эти свойства происходят из определения соответствующего набора EntitySet, которое приведено в файле SSDL.  
  
### Использование примитивных типов  
 Если в деревьях выходных команд имеются ссылки на примитивные типы, они, как правило, упоминаются в примитивных типах концептуальной модели.  Однако, применительно к определенным выражениям, поставщикам требуется соответствующий примитивный тип хранилища.  Примеры таких выражений включают DbCastExpression и, возможно, DbNullExpression, если поставщик должен привести значение NULL к соответствующему типу.  В этих случаях поставщики должны выполнить сопоставление с типом поставщика с учетом разновидности примитивного типа и его аспектов.  
  
## См. также  
 [Создание SQL](../../../../../docs/framework/data/adonet/ef/sql-generation.md)