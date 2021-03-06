---
title: "x:Code Intrinsic XAML Type | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "Code"
  - "x:Code"
  - "xCode"
helpviewer_keywords: 
  - "Code directive in XAML [XAML Services]"
  - "x:Code XAML directive element [XAML Services]"
  - "XAML [XAML Services], x:Code directive element"
ms.assetid: 87986b13-1a2e-4830-ae36-15f9dc5629e8
caps.latest.revision: 19
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 19
---
# x:Code Intrinsic XAML Type
Разрешает размещение кода в создание XAML.  Такой код может быть скомпилирован либо с любой реализацией процессора XAML, которая компилирует код XAML, либо оставлен в создании XAML для использования в дальнейшем, например для интерпретации в среде выполнения.  
  
## Использование элемента объекта XAML  
  
```  
<x:Code>  
   // code instructions, usually enclosed by CDATA...  
</x:Code>  
```  
  
## Заметки  
 Код внутри элемента директивы `x:Code` XAML по\-прежнему интерпретируется в общем пространстве имен XML и в предоставленных пространствах имен XML.  Таким образом, обычно требуется также заключить код, используемый для элемента `x:Code`, внутрь сегмента `CDATA`.  
  
 `x:Code` не разрешен для всех возможных механизмов развертывания создания XAML.  В конкретных платформах \(например, WPF\) необходимо скомпилировать код.  В других платформах использование `x:Code` может в общем случае быть запрещено.  
  
 Для платформ, разрешающих использование управляемого содержимого `x:Code`, правильный компилятор языка для содержимого `x:Code` определяется параметрами и целевыми объектами содержащего проекта, который используется для компиляции приложения.  
  
## Примечания об использовании WPF  
 Код, объявленный внутри `x:Code` для WPF, имеет несколько существенных ограничений:  
  
-   Элемент директивы `x:Code` должен быть непосредственным дочерним элементом корневого элемента создания XAML.  
  
-   [x:Class Directive](../../../docs/framework/xaml-services/x-class-directive.md) должна указываться в родительском корневом элементе.  
  
-   Код, помещенный в элемент `x:Code`, будет при компиляции рассматриваться как помещенный внутрь области разделяемого класса, который уже создан для этой страницы XAML.  Таким образом, весь определяемый код должен относиться к членам или переменным этого разделяемого класса.  
  
-   Определить дополнительные классы можно только вложением класса внутрь разделяемого класса \(выполнять вложение разрешено, однако такой подход не является типичным, поскольку на вложенные классы нельзя ссылаться в XAML\).  Невозможно определить или добавить другие пространства имен CLR, кроме используемого для существующего разделяемого класса пространства имен.  
  
-   Ссылки на сущности кода за пределами пространства имен CLR разделяемого класса должны иметь полное имя.  Если объявляемые члены переопределяют члены разделяемого класса, то это должно быть указано с помощью ключевого слова переопределения для конкретного языка.  Если члены, объявленные в области `x:Code`, конфликтуют с членами разделяемого класса, созданного вне XAML, и компилятор сообщает об этом, то файл XAML не может быть загружен или скомпилирован.  
  
## См. также  
 [x:Class Directive](../../../docs/framework/xaml-services/x-class-directive.md)   
 [Код программной части и XAML в WPF](../../../ocs/framework/wpf/advanced/code-behind-and-xaml-in-wpf.md)   
 [Общие сведения о языке XAML \(WPF\)](../../../ocs/framework/wpf/advanced/xaml-overview-wpf.md)