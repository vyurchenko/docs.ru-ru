---
title: "Отражение и машинный код .NET | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 91c9eae4-c641-476c-a06e-d7ce39709763
caps.latest.revision: 16
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 16
---
# Отражение и машинный код .NET
В платформа.NET Framework управляемая разработка поддерживает метапрограммирование через интерфейс API отражения.  Отражение позволяет проверять объекты в приложении, вызывать методы для объектов, обнаруженные в результате проверки, создавать новые типы во время выполнения и поддерживает множество других сценариев динамического кода.  Оно также поддерживает сериализацию и десериализацию, позволяющую сохранять значения полей объекта и восстанавливать их позже.  Все эти сценарии требуют использования JIT\-компилятора платформы .NET Framework для генерации машинного кода на основе имеющихся метаданных.  
  
 Среда выполнения [!INCLUDE[net_native](../../../includes/net-native-md.md)] не включает JIT\-компилятор.  В результате все необходимые машинные коды должны быть созданы заранее.  Используется набор эвристических правил, чтобы определить, какой код должен создаваться, но они не могут охватывать все возможные сценарии метапрограммирования.  Таким образом, необходимо предоставить подсказки для этих сценариев метапрограммирования с помощью [директив среды выполнения](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md).  Если необходимые метаданные или код реализации недоступны во время выполнения, приложение вызывает исключение [MissingMetadataException](../../../docs/framework/net-native/missingmetadataexception-class-net-native.md), [MissingRuntimeArtifactException](../../../docs/framework/net-native/missingruntimeartifactexception-class-net-native.md) или [MissingInteropDataException](../../../docs/framework/net-native/missinginteropdataexception-class-net-native.md).  Существуют два средства устранения неполадок, создающие соответствующую запись для файла директив среды выполнения, который устраняет исключение.  
  
-   [Средство устранения неполадок MissingMetadataException](http://dotnet.github.io/native/troubleshooter/type.html) для типов.  
  
-   [Средство устранения неполадок MissingMetadataException](http://dotnet.github.io/native/troubleshooter/method.html) для методов.  
  
> [!NOTE]
>  Общие сведения о процессе компиляции машинного кода .NET, обосновывающие необходимость файла директив среды выполнения, см. в разделе [Машинный код .NET и компиляция](../../../docs/framework/net-native/net-native-and-compilation.md).  
  
 Кроме того [!INCLUDE[net_native](../../../includes/net-native-md.md)] не позволяет выполнить отражение через закрытые члены библиотеки классов платформы .NET Framework.  Например, вызов свойства <xref:System.Reflection.TypeInfo.DeclaredFields%2A?displayProperty=fullName> для извлечения полей типа библиотеки классов платформы .NET Framework возвращает только открытые или защищенные поля.  
  
 В следующих разделах содержится основная и справочная документация, которая может потребоваться для поддержки отражения и сериализации в приложениях:  
  
-   [API\-интерфейсы, основанные на отражении](../../../docs/framework/net-native/apis-that-rely-on-reflection.md)  
  
-   [Справочник по API отражения](../../../docs/framework/net-native/net-native-reflection-api-reference.md)  
  
-   [Ссылка на файл конфигурации директив среды выполнения \(rd.xml\)](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md)  
  
## См. также  
 [Компиляция приложений с помощью машинного кода .NET](../../../docs/framework/net-native/index.md)   
 [Машинный код .NET и компиляция](../../../docs/framework/net-native/net-native-and-compilation.md)