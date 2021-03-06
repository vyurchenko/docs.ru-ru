---
title: "Запросы к службе данных (службы WCF Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-oob"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "WCF Data Services, доступ к данным"
  - "WCF Data Services, клиентская библиотека"
  - "WCF Data Services, запрос"
ms.assetid: 823e9444-27aa-4f1f-be8e-0486d67f54c0
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Запросы к службе данных (службы WCF Data Services)
Клиентская библиотека служб [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] позволяет выполнять запросы службы данных, используя знакомые шаблоны программирования [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)], включая использование языка LINQ.  Клиентская библиотека преобразует запрос, определенный на клиенте как экземпляр класса <xref:System.Data.Services.Client.DataServiceQuery%601>, в сообщение запроса HTTP GET.  Библиотека получает ответное сообщение и преобразует его в экземпляры классов клиентской службы данных.  Эти классы отслеживаются с помощью <xref:System.Data.Services.Client.DataServiceContext>, которому принадлежит объект <xref:System.Data.Services.Client.DataServiceQuery%601>.  
  
## Запросы к службе данных  
 Универсальный класс <xref:System.Data.Services.Client.DataServiceQuery%601> представляет запрос, который возвращает коллекцию, включающую ноль или больше экземпляров типа сущности.  Запрос к службе данных всегда относится к контексту существующей службы данных.  Этот контекст поддерживает URI службы и сведения о метаданных, необходимые для создания и выполнения запроса.  
  
 Если используется диалоговое окно **Добавление ссылки на службу**, чтобы добавить службу данных в клиентское приложение на основе [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)], создается класс контейнера сущностей, который наследует от <xref:System.Data.Services.Client.DataServiceContext>.  Этот класс включает свойства, возвращаемые типизированными экземплярами <xref:System.Data.Services.Client.DataServiceQuery%601>.  Для каждого набора сущностей, предоставляемого службой данных, имеется одно свойство.  Эти свойства облегчают создание экземпляра типизированного объекта <xref:System.Data.Services.Client.DataServiceQuery%601>.  
  
 Запрос выполняется в следующих сценариях.  
  
-   Если результаты перечислены неявно, например:  
  
    -   Если свойство <xref:System.Data.Services.Client.DataServiceContext>, которое представляет набор сущностей, перечисляется, например, во время цикла `foreach` \(C\#\) или `For Each` \([!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)]\).  
  
    -   Если запрос назначен коллекции `List`.  
  
-   Если метод <xref:System.Data.Services.Client.DataServiceQuery%601.Execute%2A> или <xref:System.Data.Services.Client.DataServiceQuery%601.BeginExecute%2A> вызывается явно.  
  
-   При вызове оператора выполнения запроса LINQ, такого как <xref:System.Linq.Enumerable.First%2A> или <xref:System.Linq.Enumerable.Single%2A>.  
  
 Следующий запрос, если он выполняется, возвращает все сущности `Customers` в службе данных Northwind:  
  
 [!code-csharp[Astoria Northwind Client#GetAllCustomersSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#getallcustomersspecific)]
 [!code-vb[Astoria Northwind Client#GetAllCustomersSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#getallcustomersspecific)]  
  
 Для получения дополнительной информации см. [Как выполнять запросы к службе данных](../../../../docs/framework/data/wcf/how-to-execute-data-service-queries-wcf-data-services.md).  
  
 Клиент [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] поддерживает запросы для объектов, которые будут связаны в дальнейшем, например если используется модификатор типа *dynamic* в языке C\#.  Тем не менее в силу влияния на производительность для службы данных необходимо всегда составлять строго типизированные запросы.  Тип <xref:System.Tuple> и динамические объекты не поддерживаются клиентом.  
  
## Запросы LINQ  
 Поскольку класс <xref:System.Data.Services.Client.DataServiceQuery%601> реализует интерфейс <xref:System.Linq.IQueryable%601>, определяемый языком LINQ, клиентская библиотека [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] может преобразовывать запросы LINQ к данным набора сущностей в URI, который представляет выражение запроса, вычисляемое для ресурса службы данных.  В следующем примере показан запрос LINQ, эквивалентный предыдущему объекту <xref:System.Data.Services.Client.DataServiceQuery%601>, который возвращает объект `Orders` со стоимостью транспортировки более 30 долларов и упорядочивает результаты по стоимости транспортировки.  
  
 [!code-csharp[Astoria Northwind Client#AddQueryOptionsLinqSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#addqueryoptionslinqspecific)]
 [!code-vb[Astoria Northwind Client#AddQueryOptionsLinqSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#addqueryoptionslinqspecific)]  
  
 Этот запрос LINQ преобразуется в следующий URI запроса, который выполняется для основанной на Northwind службы данных [quickstart](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md):  
  
```  
http://localhost:12345/Northwind.svc/Orders?Orderby=ShippedDate&?filter=Freight gt 30  
```  
  
> [!NOTE]
>  Набор запросов, которые можно выразить в синтаксисе LINQ, шире, чем набор запросов, поддерживаемых в URI\-синтаксисе на основе технологии REST, который используется в службах данных.  Исключение <xref:System.NotSupportedException> возникает, если запрос не может быть сопоставлен с URI в целевой службе данных.  
  
 Для получения дополнительной информации см. [Рекомендации по LINQ](../../../../docs/framework/data/wcf/linq-considerations-wcf-data-services.md).  
  
## Добавление параметров запроса  
 Запросы службы данных поддерживают все параметры запроса, которые предоставляют службы [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)].  Метод <xref:System.Data.Services.Client.DataServiceQuery%601.AddQueryOption%2A> вызывается для присоединения параметров запроса к экземпляру <xref:System.Data.Services.Client.DataServiceQuery%601>.  <xref:System.Data.Services.Client.DataServiceQuery%601.AddQueryOption%2A> возвращает новый экземпляр <xref:System.Data.Services.Client.DataServiceQuery%601>, эквивалентный исходному запросу, но с новым набором параметров запроса.  Следующий запрос, если он выполняется, возвращает объект `Orders`, отфильтрованный по значению `Freight` и упорядоченный по `OrderID` по убыванию.  
  
 [!code-csharp[Astoria Northwind Client#AddQueryOptionsSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#addqueryoptionsspecific)]
 [!code-vb[Astoria Northwind Client#AddQueryOptionsSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#addqueryoptionsspecific)]  
  
 Параметр запроса `$orderby` можно использовать как для упорядочения, так и для фильтрации запроса, основанного на одном свойстве, как в следующем примере, в котором фильтруются и упорядочиваются возвращаемые объекты `Orders`, основанные на значении свойства `Freight`:  
  
 [!code-csharp[Astoria Northwind Client#OrderWithFilter](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#orderwithfilter)]
 [!code-vb[Astoria Northwind Client#OrderWithFilter](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#orderwithfilter)]  
  
 Можно последовательно вызывать метод <xref:System.Data.Services.Client.DataServiceQuery%601.AddQueryOption%2A>, чтобы сконструировать сложные выражения запроса.  Для получения дополнительной информации см. [Как добавить параметры запросов в запрос к службе данных](../../../../docs/framework/data/wcf/how-to-add-query-options-to-a-data-service-query-wcf-data-services.md).  
  
 Параметры запроса предоставляют другой способ выражения синтаксических компонентов запроса LINQ.  Для получения дополнительной информации см. [Рекомендации по LINQ](../../../../docs/framework/data/wcf/linq-considerations-wcf-data-services.md).  
  
> [!NOTE]
>  Параметр запроса `$select` нельзя добавить в URI\-запрос с помощью метода <xref:System.Data.Services.Client.DataServiceQuery%601.AddQueryOption%2A>.  Рекомендуется использовать метод <xref:System.Linq.Enumerable.Select%2A> на основе LINQ для создания параметра запроса `$select` в URI\-запросе.  
  
<a name="executingQueries"></a>   
## Клиент и запуск сервера  
 Клиент выполняет запрос в два этапа.  По возможности сначала вычисляются выражения в запросе на стороне клиента, а затем создается URI\-запрос, который будет отправлен службе данных для проведения вычислений по отношению к данным в службе.  Рассмотрим следующий запрос LINQ:  
  
 [!code-csharp[Astoria Northwind Client#LinqQueryClientEvalSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#linqqueryclientevalspecific)]
 [!code-vb[Astoria Northwind Client#LinqQueryClientEvalSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#linqqueryclientevalspecific)]  
  
 В этом примере выражение `(basePrice – (basePrice * discount))` вычисляется на стороне клиента.  По этой причине фактический URI\-запрос `http://localhost:12345/northwind.svc/Products()?$filter=(UnitPrice gt 90.00M) and substringof('bike',ProductName)`, отправляемый службе данных, содержит уже вычисленное десятичное значение `90` в предложении фильтра.  Другие части выражения фильтрации, включая выражение подстроки, вычисляются службой данных.  Выражения, вычисляемые на стороне клиента, соответствуют семантике языка среды CLR, в то время как выражения, отправляемые службе данных, зависят от реализации протокола [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] службой данных.  Также следует помнить о сценариях, в которых это отдельное вычисление может привести к непредвиденным результатам, например если клиент и служба выполняют временные вычисления в разных часовых поясах.  
  
## Ответы на запросы  
 При выполнении запроса <xref:System.Data.Services.Client.DataServiceQuery%601> он возвращает объект <xref:System.Collections.Generic.IEnumerable%601> запрошенного типа сущности.  Этот результат запроса может быть приведен к объекту <xref:System.Data.Services.Client.QueryOperationResponse%601>, как в следующем примере:  
  
 [!code-csharp[Astoria Northwind Client#GetResponseSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#getresponsespecific)]
 [!code-vb[Astoria Northwind Client#GetResponseSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#getresponsespecific)]  
  
 Экземпляры типа сущности, которые представляют сущности в службе данных, создаются на клиенте процессом, называемым материализацией объектов.  Для получения дополнительной информации см. [Материализация объектов](../../../../docs/framework/data/wcf/object-materialization-wcf-data-services.md).  Объект <xref:System.Data.Services.Client.QueryOperationResponse%601> реализует объект <xref:System.Collections.Generic.IEnumerable%601> для предоставления доступа к результатам запроса.  
  
 Объект <xref:System.Data.Services.Client.QueryOperationResponse%601> имеет также следующие члены, позволяющие производить доступ к дополнительным сведениям о результате запроса.  
  
-   <xref:System.Data.Services.Client.OperationResponse.Error%2A> — возвращает ошибку, инициируемую операцией, если ошибка возникает.  
  
-   <xref:System.Data.Services.Client.OperationResponse.Headers%2A> — содержит коллекцию заголовков ответов HTTP, связанных с ответом на запрос.  
  
-   <xref:System.Data.Services.Client.QueryOperationResponse.Query%2A> — возвращает исходный объект <xref:System.Data.Services.Client.DataServiceQuery%601>, создавший ответ <xref:System.Data.Services.Client.QueryOperationResponse%601>.  
  
-   <xref:System.Data.Services.Client.OperationResponse.StatusCode%2A> — возвращает код ответа HTTP для ответа на запрос.  
  
-   <xref:System.Data.Services.Client.QueryOperationResponse%601.TotalCount%2A> — возвращает общее число сущностей в наборе сущностей, если метод <xref:System.Data.Services.Client.DataServiceQuery%601.IncludeTotalCount%2A> вызван на клиенте <xref:System.Data.Services.Client.DataServiceQuery%601>.  
  
-   <xref:System.Data.Services.Client.QueryOperationResponse.GetContinuation%2A> — возвращает объект <xref:System.Data.Services.Client.DataServiceQueryContinuation>, который содержит URI следующей страницы результатов.  
  
 По умолчанию службы [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] возвращают только данные, явно выбранные URI запроса.  Это дает возможность явно загрузить дополнительные данные из службы данных, если это необходимо.  Запрос отправляется в службу данных при каждой явной загрузке данных из службы данных.  Данные, которые можно явно загрузить, включают связанные сущности, разбитые на страницы данные ответа и потоки двоичных данных.  
  
> [!NOTE]
>  Поскольку служба данных может возвратить разбитый на страницы ответ, рекомендуется, чтобы приложение использовало шаблон программирования для обработки разбитого на страницы ответа службы данных.  Для получения дополнительной информации см. [Загрузка отложенного содержимого](../../../../docs/framework/data/wcf/loading-deferred-content-wcf-data-services.md).  
  
 Объем возвращаемых запросом данных может быть также уменьшен указанием, что в ответе возвращаются только определенные свойства сущности.  Для получения дополнительной информации см. [Проекции запросов](../../../../docs/framework/data/wcf/query-projections-wcf-data-services.md).  
  
## Получение подсчета общего числа сущностей в наборе  
 В некоторых сценариях полезно знать общее число сущностей в наборе сущностей, а не только число, возвращаемое запросом.  Вызовите метод <xref:System.Data.Services.Client.DataServiceQuery%601.IncludeTotalCount%2A> по отношению к объекту <xref:System.Data.Services.Client.DataServiceQuery%601> для запроса, чтобы этот общий итог подсчета сущностей в наборе возвращался с результатом запроса.  В этом случае свойство <xref:System.Data.Services.Client.QueryOperationResponse%601.TotalCount%2A> возвращаемого объекта <xref:System.Data.Services.Client.QueryOperationResponse%601> возвращает общее количество сущностей в наборе.  
  
 Можно также получить только общее число сущностей в наборе либо как значение типа <xref:System.Int32>, либо как значение типа <xref:System.Int64>, вызвав метод <xref:System.Linq.Enumerable.Count%2A> или <xref:System.Linq.Enumerable.LongCount%2A> соответственно.  Если вызываются эти методы, объект <xref:System.Data.Services.Client.QueryOperationResponse%601> не возвращается, при этом возвращается только значение подсчета.  Для получения дополнительной информации см. [Как определить количество сущностей, возвращенных запросом](../../../../docs/framework/data/wcf/number-of-entities-returned-by-a-query-wcf.md).  
  
## Содержание  
 [Проекции запросов](../../../../docs/framework/data/wcf/query-projections-wcf-data-services.md)  
  
 [Материализация объектов](../../../../docs/framework/data/wcf/object-materialization-wcf-data-services.md)  
  
 [Рекомендации по LINQ](../../../../docs/framework/data/wcf/linq-considerations-wcf-data-services.md)  
  
 [Как выполнять запросы к службе данных](../../../../docs/framework/data/wcf/how-to-execute-data-service-queries-wcf-data-services.md)  
  
 [Как добавить параметры запросов в запрос к службе данных](../../../../docs/framework/data/wcf/how-to-add-query-options-to-a-data-service-query-wcf-data-services.md)  
  
 [Как определить количество сущностей, возвращенных запросом](../../../../docs/framework/data/wcf/number-of-entities-returned-by-a-query-wcf.md)  
  
 [Как указать учетные данные клиента для запроса службы данных](../../../../docs/framework/data/wcf/specify-client-creds-for-a-data-service-request-wcf.md)  
  
 [Как установить заголовки в клиентском запросе](../../../../docs/framework/data/wcf/how-to-set-headers-in-the-client-request-wcf-data-services.md)  
  
 [Как проецировать результаты запроса](../../../../docs/framework/data/wcf/how-to-project-query-results-wcf-data-services.md)  
  
## См. также  
 [Клиентская библиотека служб WCF Data Services](../../../../docs/framework/data/wcf/wcf-data-services-client-library.md)