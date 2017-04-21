---
title: "Поставщик отражения (службы WCF Data Services) | Microsoft Docs"
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
  - "Службы WCF Data Services, поставщики"
ms.assetid: ef5ba300-6d7c-455e-a7bd-d0cc6d211ad4
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# Поставщик отражения (службы WCF Data Services)
Помимо предоставления данных из модели данных через Entity Framework, службы [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] поддерживают предоставление данных, не определенных строго в модели на основе сущностей.  Поставщик отражения предоставляет данные в классах, возвращаемые типы которых реализуют интерфейс <xref:System.Linq.IQueryable%601>.  Службы [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] используют отражение для определения модели данных для таких классов и поддерживают преобразование запросов к таким ресурсам на основе адресов в интегрированные в язык запросы \(LINQ\) к предоставляемым типам <xref:System.Linq.IQueryable%601>.  
  
> [!NOTE]
>  Метод <xref:System.Linq.Queryable.AsQueryable%2A> позволяет получить интерфейс <xref:System.Linq.IQueryable%601> любого класса, реализующего интерфейс <xref:System.Collections.Generic.IEnumerable%601>.  Это позволяет использовать большинство типов универсальных коллекций в качестве источника данных для службы данных.  
  
 Поставщик отражения поддерживает иерархии типов.  Для получения дополнительной информации см. [Как создать службу данных с помощью поставщика отражения](../../../../docs/framework/data/wcf/create-a-data-service-using-rp-wcf-data-services.md).  
  
## Выведение модели данных  
 При создании службы данных поставщик выводит модель данных при помощи отражения.  В следующем списке показано, как поставщик отражения выводит модель данных.  
  
-   Контейнер сущностей — класс, предоставляющий данные в виде свойств, возвращаемых экземпляром <xref:System.Linq.IQueryable%601>.  При обращении к модели данных на основе отражения контейнер сущностей представляет корневой объект службы.  В одном пространстве имен поддерживается только один класс контейнера сущностей.  
  
-   Наборы сущностей — свойства, возвращаемые экземплярами <xref:System.Linq.IQueryable%601>, которые рассматриваются как наборы сущностей.  Наборы сущностей непосредственно адресуются в запросе как ресурсы.  Только одно свойство контейнера сущностей может возвращать экземпляр <xref:System.Linq.IQueryable%601> данного типа.  
  
-   Типы сущностей — тип `T` объекта <xref:System.Linq.IQueryable%601>, возвращаемого набором сущностей  Классы, являющиеся частью иерархии наследования, преобразуются поставщиком отражения в эквивалентную иерархию типов сущностей.  
  
-   Ключи сущностей — каждый класс данных, определяющий тип сущности, должен иметь ключевое свойство.  Это свойство помечается с помощью атрибута <xref:System.Data.Services.Common.DataServiceKeyAttribute> \(`[DataServiceKeyAttribute]`\).  
  
    > [!NOTE]
    >  Атрибут <xref:System.Data.Services.Common.DataServiceKeyAttribute> следует применять только к сущностям, которые могут быть использованы для уникальной идентификации экземпляра типа сущности.  При применении к свойству навигации этот атрибут игнорируется.  
  
-   Свойства типов сущностей — помимо ключа сущности, поставщик отражения рассматривает их как доступные свойства \(не индексаторы\) класса, представляющего тип сущности, следующим образом.  
  
    -   Если свойство возвращает примитивный тип, оно рассматривается как свойство типа сущности.  
  
    -   Если свойство возвращает тип, который также является типом сущности, то оно рассматривается как свойство навигации, представляющее конец «один» связи «многие к одному» или «один к одному».  
  
    -   Если свойство возвращает интерфейс <xref:System.Collections.Generic.IEnumerable%601> типа сущности, оно рассматривается как свойство навигации, представляющее конец «многие» связи «один ко многим» или «многие ко многим».  
  
    -   Если тип возвращаемого значения свойства — тип значения, то свойство представляет сложный тип.  
  
> [!NOTE]
>  В отличие от модели данных, основанной на реляционной модели сущностей, модели, основанные на поставщике отражения, не поддерживают реляционные данные.  Для предоставления реляционных данных через службы [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] необходимо использовать Entity Framework.  
  
## Сопоставление типов данных  
 Если модель данных выводится из классов .NET Framework, типы\-примитивы модели данных сопоставляются с типами данных .NET Framework следующим образом.  
  
|Тип данных .NET Framework|Тип модели данных|  
|-------------------------------|-----------------------|  
|<xref:System.Byte> `[]`|`Edm.Binary`|  
|<xref:System.Boolean>|`Edm.Boolean`|  
|<xref:System.Byte>|`Edm.Byte`|  
|<xref:System.DateTime>|`Edm.DateTime`|  
|<xref:System.Decimal>|`Edm.Decimal`|  
|<xref:System.Double>|`Edm.Double`|  
|<xref:System.Guid>|`Edm.Guid`|  
|<xref:System.Int16>|`Edm.Int16`|  
|<xref:System.Int32>|`Edm.Int32`|  
|<xref:System.Int64>|`Edm.Int64`|  
|<xref:System.SByte>|`Edm.SByte`|  
|<xref:System.Single>|`Edm.Single`|  
|<xref:System.String>|`Edm.String`|  
  
> [!NOTE]
>  Типы значений платформы .NET Framework, допускающие значения NULL, сопоставляются с теми же типами модели данных, что и соответствующие типы значений, не принимающие значения NULL.  
  
## Включение обновлений в модели данных  
 Чтобы разрешить обновление данных, представляемых этим типом модели данных, поставщик отражения определяет интерфейс <xref:System.Data.Services.IUpdatable>.  Этот интерфейс описывает метод сохранения обновлений, предоставляемых службой данных типов.  Чтобы включить обновление ресурсов, определенных в модели данных, класс контейнера сущностей должен реализовать интерфейс <xref:System.Data.Services.IUpdatable>.  Пример реализации интерфейса <xref:System.Data.Services.IUpdatable> см. в разделе [Как создать службу данных с помощью источника данных LINQ to SQL](../../../../docs/framework/data/wcf/create-a-data-service-using-linq-to-sql-wcf.md).  
  
 Интерфейс <xref:System.Data.Services.IUpdatable> требует реализации следующих элементов для распространения обновлений источника данных с помощью поставщика отражения.  
  
|Член|Описание|  
|----------|--------------|  
|<xref:System.Data.Services.IUpdatable.AddReferenceToCollection%2A>|Предоставляет функциональность добавления объекта в коллекцию связанных объектов, доступ к которым осуществляется через свойство навигации.|  
|<xref:System.Data.Services.IUpdatable.ClearChanges%2A>|Предоставляет функциональность отмены отложенных изменений данных.|  
|<xref:System.Data.Services.IUpdatable.CreateResource%2A>|Предоставляет функциональность создания нового ресурса в указанном контейнере.|  
|<xref:System.Data.Services.IUpdatable.DeleteResource%2A>|Предоставляет функциональность удаления ресурса.|  
|<xref:System.Data.Services.IUpdatable.GetResource%2A>|Предоставляет функциональность извлечения ресурса, идентифицированного указанным запросом и именем типа.|  
|<xref:System.Data.Services.IUpdatable.GetValue%2A>|Предоставляет функциональность возврата значения свойства ресурса.|  
|<xref:System.Data.Services.IUpdatable.RemoveReferenceFromCollection%2A>|Предоставляет функциональность удаления объекта из коллекции связанных объектов, доступ к которым осуществляется через свойство навигации.|  
|<xref:System.Data.Services.IUpdatable.ResetResource%2A>|Предоставляет функциональность обновления указанного ресурса.|  
|<xref:System.Data.Services.IUpdatable.ResolveResource%2A>|Предоставляет функциональность возврата ресурса, представленного экземпляром определенного объекта.|  
|<xref:System.Data.Services.IUpdatable.SaveChanges%2A>|Предоставляет функциональность сохранения всех отложенных изменений.|  
|<xref:System.Data.Services.IUpdatable.SetReference%2A>|Предоставляет функциональность задания ссылки на связанный объект с помощью свойства навигации.|  
|<xref:System.Data.Services.IUpdatable.SetValue%2A>|Предоставляет функциональность задания значения свойства ресурса.|  
  
## Обработка параллелизма  
 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] поддерживает модель оптимистичного параллелизма, позволяя определять маркер параллелизма для сущности.  Этот маркер параллелизма, включающий одно или несколько свойств сущности, используется службой данных для определения, произошло ли изменение в запрашиваемых, обновляемых или удаляемых данных.  Когда значения маркера, полученные из eTag в запросе, отличаются от текущих значений сущности, служба данных вызывает исключение.  <xref:System.Data.Services.ETagAttribute> применяется к типу сущности для определения маркера параллелизма в поставщике отражения.  Маркер параллелизма не может содержать ключевое свойство или свойство навигации.  Для получения дополнительной информации см. [Обновление службы данных](../../../../docs/framework/data/wcf/updating-the-data-service-wcf-data-services.md).  
  
## Использование запросов LINQ к SQL с помощью поставщика отражения  
 Поскольку Entity Framework изначально поддерживается по умолчанию, это рекомендованный поставщик данных для работы с реляционными данными в службах [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)].  Однако для работы с запросами LINQ к классам SQL можно использовать и поставщик отражения.  Результирующие наборы <xref:System.Data.Linq.Table%601>, возвращаемые методами класса <xref:System.Data.Linq.DataContext>, сформированного реляционным конструктором объектов LINQ to SQL, реализуют интерфейс <xref:System.Linq.IQueryable%601>.  Это позволяет поставщику отражения получать доступ к таким методам и возвращать данные сущностей с сервера SQL Server при помощи сформированных классов LINQ to SQL.  Однако, поскольку запрос LINQ to SQL не реализует интерфейс <xref:System.Data.Services.IUpdatable>, необходимо добавить разделяемый класс, расширяющий имеющийся разделяемый класс <xref:System.Data.Linq.DataContext> и определяющий реализацию интерфейса <xref:System.Data.Services.IUpdatable>.  Для получения дополнительной информации см. [Как создать службу данных с помощью источника данных LINQ to SQL](../../../../docs/framework/data/wcf/create-a-data-service-using-linq-to-sql-wcf.md).  
  
## См. также  
 [Поставщики служб данных](../../../../docs/framework/data/wcf/data-services-providers-wcf-data-services.md)