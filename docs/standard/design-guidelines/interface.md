---
title: "Разработка интерфейса | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "интерфейсы [платформа .NET Framework] рекомендации по проектированию"
  - "правила разработки типов, интерфейсы"
  - "Класс рекомендации по разработке библиотек [платформа .NET Framework] интерфейсов"
ms.assetid: a016bd18-6710-4358-9438-9f190a295392
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# Разработка интерфейса
Несмотря на то, что большинство интерфейсов API лучше всего моделируются с помощью классов и структур, существуют случаи, в которых больше подходят интерфейсов, или могут использоваться только.  
  
 Среда CLR не поддерживает множественное наследование \(т. е. классы CLR, не может наследовать от более чем одного базового класса\), но создавать типы реализовать один или несколько интерфейсов, а также наследование от базового класса. Таким образом интерфейсы часто используются для получения эффекта множественное наследование. Например <xref:System.IDisposable> — это интерфейс, позволяющий типы для поддержки disposability независимо от других иерархии наследования, в котором хочу участвовать.  
  
 Другая ситуация, в определении которых подходит интерфейс находится в создании общий интерфейс, который может поддерживать несколько типов, включая некоторые типы значений. Типы значений не может наследовать от типов, отличных от <xref:System.ValueType>, но они могут реализовывать интерфейсы, с помощью интерфейса является единственным параметром, чтобы предоставить общий базовый тип.  
  
 **✓ сделать** определить интерфейс, если требуется, чтобы некоторые общий API, которые должны поддерживаться набор типов, содержащая значение типа.  
  
 **✓ Рассмотрите ВОЗМОЖНОСТЬ** определять интерфейс, если необходима поддержка его функциональности для типов, являющихся производными от другого типа.  
  
 **ИЗБЕЖАТЬ X** использования интерфейсов\-маркеров \(интерфейсов без членов\).  
  
 Если необходимо пометить класс как наличие определенных характеристик \(маркер\), как правило, используйте настраиваемый атрибут, а не интерфейс.  
  
 **✓ сделать** предоставляют по крайней мере один тип, который является реализацией интерфейса.  
  
 Это помогает проверить дизайн интерфейса. Например <xref:System.Collections.Generic.List%601> — это реализация <xref:System.Collections.Generic.IList%601> интерфейса.  
  
 **✓ сделать** предоставляют по крайней мере один API, который использует каждый из определенных интерфейсов \(метод, используя интерфейс в качестве параметра, или свойство с типом интерфейса\).  
  
 Это помогает проверить дизайн интерфейса. Например <xref:System.Collections.Generic.List%601.Sort%2A?displayProperty=fullName> использует <xref:System.Collections.Generic.IComparer%601?displayProperty=fullName> интерфейса.  
  
 **X не** добавление членов к ранее поставленному интерфейсу.  
  
 Это нарушит реализаций интерфейса. Чтобы избежать проблемы управления версиями следует создать новый интерфейс.  
  
 За исключением ситуации, описанной в эти рекомендации следует как правило, выбирать классов, а не интерфейсов в разработке повторно используемых библиотек управляемого кода.  
  
 *Частей © 2005, 2009 корпорации Microsoft. Все права защищены.*  
  
 *Воспроизведены разрешении Пирсон образования, Inc. из [Framework рекомендации по проектированию: условные обозначения, стили и шаблоны для повторного использования библиотеки .NET, второе издание](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina и Брэд Абрамс опубликованы 22 октября 2008 г., издательство Addison\-Wesley Professional как часть цикла разработки Microsoft Windows.*  
  
## См. также  
 [Правила разработки типов](../../../docs/standard/design-guidelines/type.md)   
 [Рекомендации по проектированию Framework](../../../docs/standard/design-guidelines/index.md)