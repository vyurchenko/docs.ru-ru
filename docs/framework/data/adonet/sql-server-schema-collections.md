---
title: "Коллекции схем SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c6403cc3-d78b-4f85-bab1-ada7a3446ec5
caps.latest.revision: 5
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 5
---
# Коллекции схем SQL Server
Поставщик данных Microsoft .NET Framework для SQL Server поддерживает дополнительные коллекции схем помимо общих коллекций.  Коллекции схем незначительно меняются в зависимости от используемой версии SQL Server.  Чтобы получить список поддерживаемых коллекций схем, вызовите метод **GetSchema** без аргументов или укажите имя коллекции схем «MetaDataCollections».  При этом будет возвращена <xref:System.Data.DataTable> со списком поддерживаемых коллекций схем, число ограничений, которые каждая из них поддерживает, и число идентификационных частей, которые в них используются.  
  
## Databases  
  
|ColumnName|DataType|Описание|  
|----------------|--------------|--------------|  
|database\_name|Строковое|Имя базы данных|  
|Dbid|Int16|Идентификатор базы данных|  
|create\_date|DateTime|Дата создания базы данных.|  
  
## Foreign Keys  
  
|ColumnName|DataType|Описание|  
|----------------|--------------|--------------|  
|constraint\_catalog|Строковое|Каталог, к которому принадлежит ограничение.|  
|constraint\_schema|Строковое|Схема, которая содержит ограничение.|  
|constraint\_name|Строковое|Имя.|  
|table\_catalog|Строковое|Имя таблицы, частью которой является ограничение.|  
|table\_schema|Строковое|Схема, которая содержит таблицу.|  
|table\_name|Строковое|Имя таблицы|  
|constraint\_type|Строковое|Тип ограничения.  Допускается только ограничение «FOREIGN KEY».|  
|is\_deferrable|Строковое|Указывает, является ли ограничение допускающим задержку.  Возвращает NO.|  
|initially\_deferred|Строковое|Указывает, является ли ограничение первоначально допускающим задержку.  Возвращает NO.|  
  
## Indexes  
  
|ColumnName|DataType|Описание|  
|----------------|--------------|--------------|  
|constraint\_catalog|Строковое|Каталог, которому принадлежит индекс.|  
|constraint\_schema|Строковое|Схема, которая содержит индекс.|  
|constraint\_name|Строковое|Имя индекса.|  
|table\_catalog|Строковое|Имя таблицы, с которой связан индекс.|  
|table\_schema|Строковое|Схема, содержащая таблицу, с которой связан индекс.|  
|table\_name|Строковое|Имя таблицы.|  
  
### Indexes \(SQL Server 2008\)  
 Начиная с .NET Framework 3.5 с пакетом обновления 1 \(SP1\) и SQL Server 2008, в коллекцию схем Indexes для поддержки новых пространственных типов, файловых потоков и разреженных столбцов были добавлены указанные ниже столбцы.  Эти столбцы не поддерживаются в предыдущих версиях .NET Framework и SQL Server.  
  
|ColumnName|DataType|Описание|  
|----------------|--------------|--------------|  
|type\_desc|Строковое|Индекс имеет один из указанных ниже типов.<br /><br /> -   HEAP<br />-   CLUSTERED<br />-   NONCLUSTERED<br />-   XML<br />-   SPATIAL|  
  
## IndexColumns  
  
|ColumnName|DataType|Описание|  
|----------------|--------------|--------------|  
|constraint\_catalog|Строковое|Каталог, которому принадлежит индекс.|  
|constraint\_schema|Строковое|Схема, которая содержит индекс.|  
|constraint\_name|Строковое|Имя индекса.|  
|table\_catalog|Строковое|Имя таблицы, с которой связан индекс.|  
|table\_schema|Строковое|Схема, содержащая таблицу, с которой связан индекс.|  
|table\_name|Строковое|Имя таблицы.|  
|column\_name|Строковое|Имя таблицы, с которой связан индекс.|  
|ordinal\_position|Int32|Порядковая позиция столбца.|  
|KeyType|UInt16|Тип объекта.|  
  
## Процедуры  
  
|ColumnName|DataType|Описание|  
|----------------|--------------|--------------|  
|specific\_catalog|Строковое|Собственное имя для каталога.|  
|specific\_schema|Строковое|Определенное имя схемы.|  
|specific\_name|Строковое|Определенное имя каталога.|  
|routine\_catalog|Строковое|Каталог, которому принадлежит хранимая процедура.|  
|routine\_schema|Строковое|Схема, которая содержит хранимую процедуру.|  
|routine\_name|Строковое|Имя хранимой процедуры.|  
|routine\_type|Строковое|Возвращает значение PROCEDURE для хранимых процедур и FUNCTION для функций.|  
|created|DateTime|Время создания процедуры.|  
|last\_altered|DateTime|Время последнего изменения процедуры.|  
  
## ProcedureParameters  
  
|ColumnName|DataType|Описание|  
|----------------|--------------|--------------|  
|specific\_catalog|Строковое|Имя каталога процедуры, для которой это является параметром.|  
|specific\_schema|Строковое|Схема, содержащая процедуру, частью которой является этот параметр.|  
|specific\_name|Строковое|Имя процедуры, частью которой является этот параметр.|  
|ordinal\_position|Int16|Порядковый номер параметра, начиная с 1.  Для возвращаемого значения процедуры \- 0.|  
|parameter\_mode|Строковое|Возвращает значение IN для входного параметра, OUT для выходного параметра и INOUT для изменяемого входного параметра.|  
|is\_result|Строковое|Возвращает значение YES, если результат процедуры является результатом выполнения функции.  В противном случае возвращается значение NO.|  
|as\_locator|Строковое|Возвращает значение YES, если результат объявлен как указатель.  В противном случае возвращается значение NO.|  
|parameter\_name|Строковое|Имя параметра.  Если соответствует результату выполнения функции, то возвращается значение NULL.|  
|data\_type|Строковое|Тип данных, поддерживаемый системой.|  
|character\_maximum\_length|Int32|Максимальная длина в символах для двоичных или символьных данных.  В противном случае возвращает NULL.|  
|character\_octet\_length|Int32|Максимальная длина в байтах для двоичных или символьных данных.  В противном случае возвращает NULL.|  
|collation\_catalog|Строковое|Имя каталога параметров сортировки параметра.  Если входные данные не принадлежат ни к одному из символьных типов, возвращает значение NULL.|  
|collation\_schema|Строковое|Всегда возвращает значение NULL.|  
|collation\_name|Строковое|Имя параметров сортировки параметра.  Если входные данные не принадлежат ни к одному из символьных типов, возвращает значение NULL.|  
|character\_set\_catalog|Строковое|Имя каталога кодировки параметра.  Если входные данные не принадлежат ни к одному из символьных типов, возвращает значение NULL.|  
|character\_set\_schema|Строковое|Всегда возвращает значение NULL.|  
|character\_set\_name|Строковое|Имя кодировки параметра.  Если входные данные не принадлежат ни к одному из символьных типов, возвращает значение NULL.|  
|numeric\_precision|Byte|Точность приблизительных числовых данных, точных числовых данных, целочисленных данных или денежных данных.  В противном случае возвращает NULL.|  
|numeric\_precision\_radix|Int16|Основание системы счисления точности приблизительных числовых данных, точных числовых данных, целочисленных данных или денежных данных.  В противном случае возвращает NULL.|  
|numeric\_scale|Int32|Масштаб приблизительных числовых данных, точных числовых данных, целочисленных данных или денежных данных.  В противном случае возвращает NULL.|  
|datetime\_precision|Int16|Точность в долях секунды, если параметр имеет тип datetime или smalldatetime.  В противном случае возвращает NULL.|  
|interval\_type|Строковое|NULL.  Зарезервировано для будущего использования в SQL Server.|  
|interval\_precision|Int16|NULL.  Зарезервировано для будущего использования в SQL Server.|  
  
## Таблицы  
  
|ColumnName|DataType|Описание|  
|----------------|--------------|--------------|  
|table\_catalog|Строковое|Каталог таблицы.|  
|table\_schema|Строковое|Схема, которая содержит таблицу.|  
|table\_name|Строковое|Имя таблицы.|  
|table\_type|Строковое|Тип таблицы.  Может быть VIEW или BASE TABLE.|  
  
## Столбцы  
  
|ColumnName|DataType|Описание|  
|----------------|--------------|--------------|  
|table\_catalog|Строковое|Каталог таблицы.|  
|table\_schema|Строковое|Схема, которая содержит таблицу.|  
|table\_name|Строковое|Имя таблицы.|  
|column\_name|Строковое|Имя столбца.|  
|ordinal\_position|Int16|Идентификационный номер столбца.|  
|column\_default|Строковое|Значение столбца по умолчанию.|  
|is\_nullable|Строковое|Указывает, может ли столбец содержать значение NULL.  Если для столбца допустимо значение NULL, этот столбец возвращает значение YES.  Иначе возвращается значение NO.|  
|data\_type|Строковое|Тип данных, поддерживаемый системой.|  
|character\_maximum\_length|Int32 – Sql8, Int16 – Sql7|Максимальная длина в символах для двоичных данных, символьных данных или текстовых данных и изображений.  В противном случае возвращается значение NULL.|  
|character\_octet\_length|Int32 – SQL8, Int16 – Sql7|Максимальная длина в байтах для двоичных данных, символьных данных или текстовых данных и изображений.  В противном случае возвращается значение NULL.|  
|numeric\_precision|Unsigned Byte|Точность приблизительных числовых данных, точных числовых данных, целочисленных данных или денежных данных.  В противном случае возвращается значение NULL.|  
|numeric\_precision\_radix|Int16|Основание системы счисления точности приблизительных числовых данных, точных числовых данных, целочисленных данных или денежных данных.  В противном случае возвращается значение NULL.|  
|numeric\_scale|Int32|Масштаб приблизительных числовых данных, точных числовых данных, целочисленных данных или денежных данных.  В противном случае возвращается значение NULL.|  
|datetime\_precision|Int16|Код подтипа для типа данных datetime и типа данных interval языка SQL\-92.  Для других типов данных возвращается значение NULL.|  
|character\_set\_catalog|Строковое|Возвращает значение «master», т. е. имя базы данных, в которой находится кодировка, если столбец имеет символьный тип данных или текстовый тип данных.  В противном случае возвращается значение NULL.|  
|character\_set\_schema|Строковое|Всегда возвращает значение NULL.|  
|character\_set\_name|Строковое|Возвращает уникальное имя для кодировки, если столбец содержит символьные данные или текстовые данные.  В противном случае возвращается значение NULL.|  
|collation\_catalog|Строковое|Возвращает значение "master", т.е. имя базы данных, в которой определен параметр сортировки, если столбец имеет символьный тип данных или текстовый тип данных.  В противном случае этот столбец содержит значение NULL.|  
  
### Columns \(SQL Server 2008\)  
 Начиная с .NET Framework 3.5 с пакетом обновления 1 \(SP1\) и SQL Server 2008, в коллекцию схем Columns для поддержки новых пространственных типов, файловых потоков и разреженных столбцов были добавлены указанные ниже столбцы.  Эти столбцы не поддерживаются в предыдущих версиях .NET Framework и SQL Server.  
  
|ColumnName|DataType|Описание|  
|----------------|--------------|--------------|  
|IS\_FILESTREAM|Строковое|YES, если для столбца установлен атрибут FILESTREAM.<br /><br /> NO, если для столбца не установлен атрибут FILESTREAM.|  
|IS\_SPARSE|Строковое|YES, если столбец является разреженным.<br /><br /> NO, если столбец не является разреженным.|  
|IS\_COLUMN\_SET|Строковое|YES, если столбец является набором столбцов.<br /><br /> NO, если столбец не является набором столбцов.|  
  
### AllColumns \(SQL Server 2008\)  
 Начиная с .NET Framework 3.5 с пакетом обновления 1 \(SP1\) и SQL Server 2008, для поддержки разреженных столбцов была добавлена коллекция схем AllColumns.  Коллекция схем AllColumns не поддерживается в предыдущих версиях .NET Framework и SQL Server.  
  
 Для коллекции схем AllColumns установлены те же ограничения и результирующая схема DataTable, что и для коллекции схем Columns.  Единственное отличие заключается в том, что коллекция схем AllColumns включает столбцы, представляющие наборы столбцов, которые не входят в коллекцию схем Columns.  Эти столбцы описаны в приведенной ниже таблице.  
  
|ColumnName|DataType|Описание|  
|----------------|--------------|--------------|  
|table\_catalog|Строковое|Каталог таблицы.|  
|table\_schema|Строковое|Схема, которая содержит таблицу.|  
|table\_name|Строковое|Имя таблицы.|  
|column\_name|Строковое|Имя столбца.|  
|ordinal\_position|Int16|Идентификационный номер столбца.|  
|column\_default|Строковое|Значение столбца по умолчанию.|  
|is\_nullable|Строковое|Указывает, может ли столбец содержать значение NULL.  Если для столбца допустимо значение NULL, этот столбец возвращает значение YES.  В противном случае возвращается значение NO.|  
|data\_type|Строковое|Тип данных, поддерживаемый системой.|  
|character\_maximum\_length|Int32|Максимальная длина в символах для двоичных данных, символьных данных или текстовых данных и изображений.  В противном случае возвращается значение NULL.|  
|character\_octet\_length|Int32|Максимальная длина в байтах для двоичных данных, символьных данных или текстовых данных и изображений.  В противном случае возвращается значение NULL.|  
|numeric\_precision|Unsigned Byte|Точность приблизительных числовых данных, точных числовых данных, целочисленных данных или денежных данных.  В противном случае возвращается значение NULL.|  
|numeric\_precision\_radix|Int16|Основание системы счисления точности приблизительных числовых данных, точных числовых данных, целочисленных данных или денежных данных.  В противном случае возвращается значение NULL.|  
|numeric\_scale|Int32|Масштаб приблизительных числовых данных, точных числовых данных, целочисленных данных или денежных данных.  В противном случае возвращается значение NULL.|  
|datetime\_precision|Int16|Код подтипа для типа данных datetime и типа данных interval языка SQL\-92.  Для других типов данных возвращается значение NULL.|  
|character\_set\_catalog|Строковое|Возвращает значение «master», т. е. имя базы данных, в которой находится кодировка, если столбец имеет символьный тип данных или текстовый тип данных.  В противном случае возвращается значение NULL.|  
|character\_set\_schema|Строковое|Всегда возвращает значение NULL.|  
|character\_set\_name|Строковое|Возвращает уникальное имя для кодировки, если столбец содержит символьные данные или текстовые данные.  В противном случае возвращается значение NULL.|  
|collation\_catalog|Строковое|Возвращает значение "master", т.е. имя базы данных, в которой определен параметр сортировки, если столбец имеет символьный тип данных или текстовый тип данных.  В противном случае этот столбец содержит значение NULL.|  
|IS\_FILESTREAM|Строковое|YES, если для столбца установлен атрибут FILESTREAM.<br /><br /> NO, если для столбца не установлен атрибут FILESTREAM.|  
|IS\_SPARSE|Строковое|YES, если столбец является разреженным.<br /><br /> NO, если столбец не является разреженным.|  
|IS\_COLUMN\_SET|Строковое|YES, если столбец является набором столбцов.<br /><br /> NO, если столбец не является набором столбцов.|  
  
### ColumnSetColumns \(SQL Server 2008\)  
 Начиная с .NET Framework 3.5 с пакетом обновления 1 \(SP1\) и SQL Server 2008, для поддержки разреженных столбцов была добавлена коллекция схем ColumnSetColumns.  Коллекция схем ColumnSetColumns не поддерживается в предыдущих версиях .NET Framework и SQL Server.  Коллекция схем ColumnSetColumns возвращает схему для всех столбцов в наборе столбцов.  Эти столбцы описаны в приведенной ниже таблице.  
  
|ColumnName|DataType|Описание|  
|----------------|--------------|--------------|  
|table\_catalog|Строковое|Каталог таблицы.|  
|table\_schema|Строковое|Схема, которая содержит таблицу.|  
|table\_name|Строковое|Имя таблицы.|  
|column\_name|Строковое|Имя столбца.|  
|ordinal\_position|Int16|Идентификационный номер столбца.|  
|column\_default|Строковое|Значение столбца по умолчанию.|  
|is\_nullable|Строковое|Указывает, может ли столбец содержать значение NULL.  Если для столбца допустимо значение NULL, этот столбец возвращает значение YES.  В противном случае возвращается значение NO.|  
|data\_type|Строковое|Тип данных, поддерживаемый системой.|  
|character\_maximum\_length|Int32|Максимальная длина в символах для двоичных данных, символьных данных или текстовых данных и изображений.  В противном случае возвращается значение NULL.|  
|character\_octet\_length|Int32|Максимальная длина в байтах для двоичных данных, символьных данных или текстовых данных и изображений.  В противном случае возвращается значение NULL.|  
|numeric\_precision|Unsigned Byte|Точность приблизительных числовых данных, точных числовых данных, целочисленных данных или денежных данных.  В противном случае возвращается значение NULL.|  
|numeric\_precision\_radix|Int16|Основание системы счисления точности приблизительных числовых данных, точных числовых данных, целочисленных данных или денежных данных.  В противном случае возвращается значение NULL.|  
|numeric\_scale|Int32|Масштаб приблизительных числовых данных, точных числовых данных, целочисленных данных или денежных данных.  В противном случае возвращается значение NULL.|  
|datetime\_precision|Int16|Код подтипа для типа данных datetime и типа данных interval языка SQL\-92.  Для других типов данных возвращается значение NULL.|  
|character\_set\_catalog|Строковое|Возвращает значение «master», т. е. имя базы данных, в которой находится кодировка, если столбец имеет символьный тип данных или текстовый тип данных.  В противном случае возвращается значение NULL.|  
|character\_set\_schema|Строковое|Всегда возвращает значение NULL.|  
|character\_set\_name|Строковое|Возвращает уникальное имя для кодировки, если столбец содержит символьные данные или текстовые данные.  В противном случае возвращается значение NULL.|  
|collation\_catalog|Строковое|Возвращает значение "master", т.е. имя базы данных, в которой определен параметр сортировки, если столбец имеет символьный тип данных или текстовый тип данных.  В противном случае этот столбец содержит значение NULL.|  
|IS\_FILESTREAM|Строковое|YES, если для столбца установлен атрибут FILESTREAM.<br /><br /> NO, если для столбца не установлен атрибут FILESTREAM.|  
|IS\_SPARSE|Строковое|YES, если столбец является разреженным.<br /><br /> NO, если столбец не является разреженным.|  
|IS\_COLUMN\_SET|Строковое|YES, если столбец является набором столбцов.<br /><br /> NO, если столбец не является набором столбцов.|  
  
## Users  
  
|ColumnName|DataType|Описание|  
|----------------|--------------|--------------|  
|uid|Int16|Идентификатор пользователя, уникальный в этой базе данных.  1 — это владелец базы данных.|  
|имя|Строковое|Имя пользователя или имя группы, уникальные в этой базе данных.|  
|createdate|DateTime|Дата добавления этой учетной записи.|  
|updatedate|DateTime|Дата последнего изменения учетной записи.|  
  
## Представления  
  
|ColumnName|DataType|Описание|  
|----------------|--------------|--------------|  
|table\_catalog|Строковое|Каталог представления.|  
|table\_schema|Строковое|Схема, которая содержит представление.|  
|table\_name|Строковое|Имя представления.|  
|check\_option|Строковое|Тип инструкции WITH CHECK OPTION.  CASCADE, если первоначальное представление было создано с помощью инструкции WITH CHECK OPTION.  Иначе возвращается значение NONE.|  
|is\_updatable|Строковое|Указывает, можно ли обновлять это представление.  Всегда возвращает «NO».|  
  
## ViewColumns  
  
|ColumnName|DataType|Описание|  
|----------------|--------------|--------------|  
|view\_catalog|Строковое|Каталог представления.|  
|view\_schema|Строковое|Схема, которая содержит представление.|  
|view\_name|Строковое|Имя представления.|  
|table\_catalog|Строковое|Каталог таблицы, которая связана с этим представлением.|  
|table\_schema|Строковое|Schema, который содержит таблицу, связанную с этим представлением.|  
|table\_name|Строковое|Имя таблицы, которая связана с представлением.  Базовая таблица.|  
|column\_name|Строковое|Имя столбца.|  
  
## UserDefinedTypes  
  
|ColumnName|DataType|Описание|  
|----------------|--------------|--------------|  
|assembly\_name|Строковое|Имя файла для сборки.|  
|UDT\_name|Строковое|Имя класса для сборки.|  
|version\_major|Объект|Основной номер версии.|  
|version\_minor|Объект|Дополнительный номер версии.|  
|version\_build|Объект|Номер сборки.|  
|version\_revision|Объект|Номер редакции.|  
|Culture\_info|Объект|Сведения о языке и региональных параметрах, которые связаны с этим определяемым пользователем типом.|  
|Public\_key|Объект|Открытый ключ, используемый в этой сборке.|  
|Is\_fixed\_length|Boolean|Указывает, является ли длина данных этого типа всегда равной значению max\_length.|  
|max\_length|Int16|Максимальная длина значения типа в байтах.|  
|permission\_set\_desc|Строковое|Удобное в использовании имя набора разрешений и \(или\) уровня безопасности для сборки.|  
|create\_date|DateTime|Дата создания или регистрации сборки.|  
  
## См. также  
 [Получение сведений о схеме базы данных](../../../../docs/framework/data/adonet/retrieving-database-schema-information.md)   
 [Центр разработчиков, поставщики ADO.NET Managed Provider и набор данных](http://go.microsoft.com/fwlink/?LinkId=217917)