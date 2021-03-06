---
title: "Средство поиска закрытых ключей (FindPrivateKey.exe) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
ms.assetid: b8846a95-3fcc-4e8c-b9c0-128d975a6307
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# Средство поиска закрытых ключей (FindPrivateKey.exe)
Эта программа командной строки предназначена для извлечения закрытого ключа из хранилища сертификатов.  Например, FindPrivateKey.exe можно использовать для нахождения местоположения и имени файла закрытого ключа, связанного с конкретным сертификатом X.509 в хранилище сертификатов.  
  
> [!IMPORTANT]
>  Средство FindPrivateKey поставляется в качестве образца WCF.  Дополнительные сведения о том, где найти образец и как выполнить его сборку, см. в разделе  
  
## Синтаксис  
  
```  
FindPrivateKey <storeName> <storeLocation> [{ {-n <subjectName>} | {-t <thumbprint>} } [-f | -d | -a]]  
```  
  
## Заметки  
 В следующих таблицах описаны аргументы и параметры, которые можно использовать со средством Find Private Key \(FindPrivateKey.exe\).  
  
|Аргумент|Описание|  
|--------------|--------------|  
|`storeName`|Имя хранилища сертификатов.|  
|`storeLocation`|Расположение хранилища сертификатов.|  
  
|Параметр|Описание|  
|--------------|--------------|  
|`/n <` *subjectName* `>`|Задает имя субъекта сертификата.|  
|`/t <` *thumbprint* `>`|Задает отпечаток сертификата.  Используйте Certmgr.exe для извлечения отпечатка сертификата.|  
|`/f`|Выводит только имя файла.|  
|`/d`|Выводит только каталог.|  
|`/a`|Выводит абсолютное имя файла.|  
  
## Примеры  
 Следующая команда извлекает закрытый ключ для John Doe.  
  
```  
FindPrivateKey My CurrentUser -n "CN=John Doe"  
```  
  
 Следующая команда извлекает закрытый ключ для локального компьютера.  
  
```  
FindPrivateKey My LocalMachine -t "03 33 98 63 d0 47 e7 48 71 33 62 64 76 5c 4c 9d 42 1d 6b 52" –a  
```