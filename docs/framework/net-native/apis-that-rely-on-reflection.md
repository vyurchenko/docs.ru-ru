---
title: "API-интерфейсы, основанные на отражении | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f9532629-6594-4a41-909f-d083f30a42f3
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# API-интерфейсы, основанные на отражении
В некоторых случаях использование отражения в коде не очевидно, и цепочка инструментов [!INCLUDE[net_native](../../../includes/net-native-md.md)] не сохраняет метаданные, необходимые во время выполнения.  В этом разделе рассматриваются некоторые общие интерфейсы API или распространенные шаблоны программирования, которые не считаются частью API\-интерфейса отражения, однако используют отражение для успешного выполнения.  При их использовании в исходном коде, можно добавить сведения о них в файл директив среды выполнения \(. rd.xml\), чтобы вызовы этих интерфейсов API не создавали исключений [MissingMetadataException](../../../docs/framework/net-native/missingmetadataexception-class-net-native.md) или других исключений во время выполнения.  
  
## Метод Type.MakeGenericType  
 Можно динамически создать экземпляр универсального типа `AppClass<T>` путем вызова метода <xref:System.Type.MakeGenericType%2A?displayProperty=fullName> с помощью следующего кода:  
  
 [!code-csharp[ProjectN#1](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/type_makegenerictype1.cs#1)]  
  
 Для успешной работы кода во время выполнения необходимы несколько элементов метаданных.  Во\-первых, метаданные `Browse` для универсального типа без экземпляров, `AppClass<T>`:  
  
```  
<Type Name="App1.AppClass`1" Browse="Required PublicAndInternal" />  
```  
  
 Это позволяет вызову метода <xref:System.Type.GetType%28System.String%2CSystem.Boolean%29?displayProperty=fullName> завершиться успешно и вернуть допустимый объект <xref:System.Type>.  
  
 Но даже при добавлении метаданных для универсального типа без экземпляров, вызов метода <xref:System.Type.MakeGenericType%2A?displayProperty=fullName> приводит к исключению [MissingMetadataException](../../../docs/framework/net-native/missingmetadataexception-class-net-native.md):  
  
```  
  
This operation cannot be carried out as metadata for the following type was removed for performance reasons:  
  
App1.AppClass`1<System.Int32>.  
  
```  
  
 Можно добавить следующую директиву времени выполнения в файл директив среды выполнения, чтобы добавить метаданные `Activate` для конкретного экземпляра, созданного над `AppClass<T>` из <xref:System.Int32?displayProperty=fullName>:  
  
```  
  
<TypeInstantiation Name="App1.AppClass" Arguments="System.Int32"   
                   Activate="Required Public" />  
  
```  
  
 Каждый другой экземпляр над `AppClass<T>` требует отдельной директивы, если он создается с помощью метода <xref:System.Type.MakeGenericType%2A?displayProperty=fullName>и не используется статически.  
  
## Метод MethodInfo.MakeGenericMethod  
 Определенный класс `Class1` с универсальным методом `GetMethod<T>(T t)`, `GetMethod` можно вызывать с помощью отражения, используя следующий код:  
  
 [!code-csharp[ProjectN#2](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/makegenericmethod1.cs#2)]  
  
 Для успешного выполнения этого кода необходимо несколько элементов метаданных:  
  
-   Метаданные `Browse` для типа, метод которого необходимо вызвать.  
  
-   Метаданные `Browse` для метода, который требуется вызвать.  Если это открытый метод, добавление открытых метаданных `Browse` для содержащего типа включает и сам метод.  
  
-   Динамические метаданные для метода, который необходимо вызвать, для того, чтобы делегат вызова отражения не удалялся цепочкой инструментов [!INCLUDE[net_native](../../../includes/net-native-md.md)].  В случае отсутствия динамических метаданных для метода создается следующее исключение <xref:System.Reflection.MethodInfo.MakeGenericMethod%2A?displayProperty=fullName>, когда вызывается метод:  
  
    ```  
  
    MakeGenericMethod() cannot create this generic method instantiation because the instantiation was not metadata-enabled: 'App1.Class1.GenMethod<Int32>(Int32)'.  
  
    ```  
  
 Следующие директивы среды выполнения гарантируют доступность всех необходимых метаданных:  
  
```  
  
<Type Name="App1.Class1" Browse="Required PublicAndInternal">  
   <MethodInstantiation Name="GenMethod" Arguments="System.Int32" Dynamic="Required"/>  
</Type>  
  
```  
  
 Директива `MethodInstantiation` обязательна для каждого отдельного экземпляра метода, который вызывается динамически, а элемент `Arguments` обновляется для отображения аргумента каждого отдельного экземпляра.  
  
## Методы метода Array.CreateInstance и Type.MakeTypeArray  
 В следующем примере вызываются методы <xref:System.Type.MakeArrayType%2A?displayProperty=fullName> и <xref:System.Array.CreateInstance%2A?displayProperty=fullName> на типе `Class1`.  
  
 [!code-csharp[ProjectN#3](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/array1.cs#3)]  
  
 При отсутствии метаданных массива возникает следующая ошибка:  
  
```  
This operation cannot be carried out as metadata for the following type was removed for performance reasons:  
  
App1.Class1[]  
  
Unfortunately, no further information is available.  
```  
  
 метаданные `Browse` для типа массива требуются для динамического создания его экземпляра.  Следующая директива среды выполнения позволяет создать динамический экземпляр `Class1[]`.  
  
```  
<Type Name="App1.Class1[]" Browse="Required Public" />  
```  
  
## См. также  
 [Начало работы](../../../docs/framework/net-native/getting-started-with-net-native.md)   
 [Ссылка на файл конфигурации директив среды выполнения \(rd.xml\)](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md)