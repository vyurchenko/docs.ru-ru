---
title: "Особенности функций Windows Workflow Foundation | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e84d12da-a055-45f6-b4d1-878d127b46b6
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Особенности функций Windows Workflow Foundation
[!INCLUDE[netfx40_long](../../../includes/netfx40-long-md.md)] добавляет ряд функциональных возможностей в Windows Workflow Foundation.В этом документе описываются некоторые новые функциональные возможности и приведены подробные сведения о сценариях, в которых они могут оказаться полезными.  
  
## Действия обмена сообщениями  
 Действия обмена сообщениями \(<xref:System.ServiceModel.Activities.Receive>, <xref:System.ServiceModel.Activities.SendReply>, <xref:System.ServiceModel.Activities.Send>, <xref:System.ServiceModel.Activities.ReceiveReply>\), служат для отправки и получения сообщений [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] в рабочем процессе. Действия <xref:System.ServiceModel.Activities.Receive> и <xref:System.ServiceModel.Activities.SendReply> служат для образования операции службы [!INCLUDE[indigo1](../../../includes/indigo1-md.md)], отображаемой с помощью WSDL в виде обычной веб\-службы [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]. Действия <xref:System.ServiceModel.Activities.Send> и <xref:System.ServiceModel.Activities.ReceiveReply> позволяют работать с такими веб\-службами, как WCF <xref:System.ServiceModel.ChannelFactory>; для технологии Workflow Foundation, создающей заранее настроенные действия, также существует возможность **Добавить ссылку на службу**.  
  
### Приступая к работе с действиями обмена сообщениями  
  
-   В [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)] создайте проект служебного приложения рабочего процесса WCF.На полотне будут расположены <xref:System.ServiceModel.Activities.Receive> и <xref:System.ServiceModel.Activities.SendReply>.  
  
-   Щелкните проект правой кнопкой мыши и выберите команду **Добавить ссылку на службу**. Выберите существующую веб\-службу WSDL и нажмите кнопку **ОК**. Создайте свой проект, чтобы созданные действия \(реализованные с помощью <xref:System.ServiceModel.Activities.Send> и <xref:System.ServiceModel.Activities.ReceiveReply>\) были показаны в области элементов.  
  
-   Образцы этих действий можно найти в следующих разделах:  
  
    -   Основы: [Службы](../../../docs/framework/windows-workflow-foundation/samples/services.md)  
  
    -   Сценарии: [Службы](../../../docs/framework/windows-workflow-foundation/samples/services.md)  
  
-   [Основная документация](http://go.microsoft.com/fwlink/?LinkId=204801)  
  
-   [Документация по конструктору действий обмена сообщениями](http://go.microsoft.com/fwlink/?LinkId=204802)  
  
### Пример сценария действий обмена сообщениями  
 Служба `BestPriceFinder` обращается к нескольким службам авиалиний, пытаясь найти по минимальной цене билеты по определенному маршруту. Для реализации этого сценария потребуется с помощью действий обмена сообщениями получить данные о ценах, извлечь цены из внутренних служб и ответа на запрос о минимальных ценах. Кроме того, потребуется с помощью других готовых действий создать бизнес\-логику для вычисления наилучшей цены.  
  
## WorkflowServiceHost  
 Класс <xref:System.ServiceModel.WorkflowServiceHost> представляет собой готовый узел рабочего процесса, поддерживающий несколько экземпляров, конфигурацию и обмен сообщениями [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] \(хотя для размещения рабочих процессов обмен сообщениями не требуется\). Он также интегрируется с функциями сохраняемости, отслеживания и управления экземпляром с помощью набора поведений служб. Так же как и <xref:System.ServiceModel.ServiceHost> в [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], <xref:System.ServiceModel.WorkflowServiceHost> может размещаться резидентно в консольном приложении, приложении WinForms или WPF, в службе Windows или в сети \(в виде XAMLX\-файла\) в службах IIS или WAS.  
  
### Приступая к работе со службой рабочего процесса  
  
-   В Visual Studio 2010 создайте проект приложения службы рабочего процесса [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]: этот проект будет настроен для использования <xref:System.ServiceModel.WorkflowServiceHost> в среде сетевого размещения.  
  
-   Чтобы разместить рабочий процесс, не связанный с обменом сообщениями, добавьте пользовательский класс <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint>, который создаст экземпляр на основе сообщения.  
  
-   Экземплярами рабочего процесса можно управлять \(например,приостанавливать или завершать их работу\) путем добавления <xref:System.ServiceModel.Activities.WorkflowControlEndpoint> в <xref:System.ServiceModel.WorkflowServiceHost> с последующим вызовом <xref:System.ServiceModel.Activities.WorkflowControlClient>.  
  
-   Образцы <xref:System.ServiceModel.WorkflowServiceHost> приведены в следующих разделах:  
  
    -   [Выполнение](../../../docs/framework/windows-workflow-foundation/samples/execution.md)  
  
    -   Основы: [Службы](../../../docs/framework/windows-workflow-foundation/samples/services.md)  
  
    -   Сценарии: [Службы](../../../docs/framework/windows-workflow-foundation/samples/services.md)  
  
    -   Приложение: [Управление приостановленным экземпляром](../../../docs/framework/windows-workflow-foundation/samples/suspended-instance-management.md)  
  
-   [Основная документация по WorkflowServiceHost](http://go.microsoft.com/fwlink/?LinkId=204807)  
  
### Сценарий WorkflowServiceHost  
 Служба BestPriceFinder обращается к нескольким службам авиалиний, пытаясь найти билет на определенный маршрут по минимальной цене. Для реализации этого сценария потребуется разместить рабочий процесс в <xref:System.ServiceModel.WorkflowServiceHost>. Действия обмена сообщениями также служат для получения запроса о цене, извлечения цен из внутренних служб и ответа на запрос наилучшей цены.  
  
## Корреляция  
 Корреляцией называют два следующих явления:  
  
-   Способ группирования сообщений, т. е. связь между сообщением с запросом и ответом на него.  
  
-   Способ сопоставления порции данных с экземпляром службы.  
  
### Приступая к работе  
  
-   Чтобы начать работу с корреляцией, создайте новый проект в Visual Studio.Создайте переменную типа <xref:System.ServiceModel.Activities.CorrelationHandle>.  
  
-   Примером корреляции для группирования сообщений является корреляция по схеме «запрос\-ответ», группирующая сообщения.  
  
    -   Для действия <xref:System.ServiceModel.Activities.Receive> щелкните свойство <xref:System.ServiceModel.Activities.Receive.CorrelationInitializers%2A> и добавьте <xref:System.ServiceModel.Activities.RequestReplyCorrelationInitializer> с помощью типа CorrelationHandle, созданного в первом шаге выше.  
  
    -   Создайте действие <xref:System.ServiceModel.Activities.SendReply>, щелкнув правой кнопкой мыши действие <xref:System.ServiceModel.Activities.Receive> и выбрав «Создать SendReply».Вставьте его в рабочий процесс после действия <xref:System.ServiceModel.Activities.Receive>.  
  
-   Примером сопоставления порции данных с экземпляром службы является корреляция на основе содержимого, сопоставляющая данные \(например, идентификатор заказа\) с определенным экземпляром рабочего процесса.  
  
    -   Для любого действия обмена сообщениями щелкните свойство `CorrelationInitializers` и добавьте <xref:System.ServiceModel.Activities.QueryCorrelationInitializer> с помощью переменной <xref:System.ServiceModel.Activities.CorrelationHandle>, созданной ранее.Дважды щелкните нужное свойство сообщения \(например,OrderID\) в раскрывающемся меню.Установите свойство `CorrelatesWith` в значение переменной <xref:System.ServiceModel.Activities.CorrelationHandle>, определенной выше.  
  
-   Образцы:  
  
    -   Основы: [Службы](../../../docs/framework/windows-workflow-foundation/samples/services.md)  
  
    -   Сценарии: [Службы](../../../docs/framework/windows-workflow-foundation/samples/services.md)  
  
    -   [Основная документация по корреляции](http://go.microsoft.com/fwlink/?LinkId=204939)  
  
### Сценарий корреляции  
 Рабочий процесс обработки заказов выполняет создание нового заказа и обновляет существующие заказы, находящиеся в процессе обработки. Для реализации этого сценария потребуется разместить рабочий процесс в <xref:System.ServiceModel.WorkflowServiceHost> и использовать действия обмена сообщениями. Это также потребует выполнения корреляции на основе `orderId`, чтобы обновления гарантированно применялись к нужному рабочему процессу.  
  
## Упрощенная конфигурация  
 Схема конфигурации [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] сложна и содержит много функций, которые трудно найти.В [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] мы постарались помочь пользователям [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] в настройке служб с помощью следующих возможностей.  
  
-   Устранена необходимость явной настройки каждой службы отдельно.Если для службы не настроено ни одного элемента \<service\> и служба не может программно определить конечные точки, то набор конечных точек будет автоматически добавлен к службе: по одной на каждый базовый адрес службы и на каждый контракт, используемый службой.  
  
-   Позволяет пользователю определять для привязок WCF и поведений значения по умолчанию, которые будут применяться к службам без явно заданной конфигурации.  
  
-   Стандартные конечные точки определяют повторно используемые, заранее настроенные конечные точки, имеющие фиксированные значения для одного или нескольких свойств \(адрес, привязка и контракт\), а также позволяют определить пользовательские свойства.  
  
-   Наконец, <xref:System.ServiceModel.Configuration.ConfigurationChannelFactory%601> позволяет централизованно управлять конфигурацией клиента [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], что может оказаться полезным в тех случаях, когда конфигурация выбирается или изменяется после времени загрузки домена приложения.  
  
### Приступая к работе  
  
-   [Руководство разработчика WCF 4.0](http://go.microsoft.com/fwlink/?LinkId=204940)  
  
-   [Производство канала настройки](http://go.microsoft.com/fwlink/?LinkId=204941)  
  
-   [Элемент стандартной конечной точки](http://go.microsoft.com/fwlink/?LinkId=204942)  
  
-   [Улучшения конфигурации службы в .Net Framework 4](http://go.microsoft.com/fwlink/?LinkId=204943)  
  
-   [Распространенная ошибка пользователей в .NET 4: опечатки в имени конфигурации служб WF и WCF](http://go.microsoft.com/fwlink/?LinkId=204944)  
  
### Сценарии упрощенной конфигурации  
  
-   Опытному разработчику ASMX необходимо начать работу с [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].Но [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] кажется чересчур сложным\!Что означает вся информация, которую нужно указать в файле конфигурации?В .NET 4 можно вообще не использовать файл конфигурации.  
  
-   Существующий набор служб WCF очень сложно настраивать и обслуживать.Файл конфигурации содержит тысячи строк XML\-кода, которые очень опасно трогать.Потребуется помощь, чтобы уменьшить объем кода и сделать его более управляемым.  
  
## Арбитр контрактов данных  
 В .NET 3.5 имелись некоторые ограничения в разработке известных типов.  
  
-   Было невозможно динамически добавлять известные типы во время сериализации и десериализации.  
  
-   Сериализаторы не могли работать с неизвестными данными в xsi:type.  
  
-   Пользователи не смогли указать xsi:type, который должен появиться в канале, например уменьшить размер экземпляра сериализации в канале.  
  
 [DataContractResolver](../../../docs/framework/wcf/samples/datacontractresolver.md) решает эти проблемы в .NET 4.5.  
  
### Начало работы  
  
-   [Документация по API арбитра контрактов данных](http://go.microsoft.com/fwlink/?LinkId=204946)  
  
-   [Представление арбитра контрактов данных](http://go.microsoft.com/fwlink/?LinkId=204947)  
  
-   Образцы:  
  
    -   [DataContractResolver](../../../docs/framework/wcf/samples/datacontractresolver.md)  
  
    -   [Атрибут KnownAssemblyAttribute](../../../docs/framework/wcf/samples/knownassemblyattribute.md)  
  
### Сценарии арбитра контрактов данных  
  
-   Как избежать необходимости объявлять десятки объектов <xref:System.Runtime.Serialization.KnownTypeAttribute> в службе.  
  
-   Уменьшение размера большого двоичного объекта XML.  
  
## Блок\-схема  
 Блок\-схема — это распространенный способ визуального представления проблем домена.Это новая разновидность потока управления, появившаяся в .NET 4.Основная особенность блок\-схемы заключается в том, что в определенное время выполняется только одно действие.Блок\-схемы могут представлять циклы и альтернативные результаты, но не могут стандартно представлять параллельное выполнение нескольких узлов.  
  
### Приступая к работе  
  
-   В [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)] создайте консольное приложение рабочего процесса.В конструкторе рабочих процессов добавьте блок\-схему.  
  
-   В блок\-схеме используются следующие классы:  
  
    -   <xref:System.Activities.Statements.Flowchart>  
  
    -   <xref:System.Activities.Statements.FlowNode>  
  
    -   <xref:System.Activities.Statements.FlowDecision>  
  
    -   <xref:System.Activities.Statements.FlowStep>  
  
    -   <xref:System.Activities.Statements.FlowSwitch%601>  
  
-   Образцы:  
  
    -   [Обработка ошибок в действии блок\-схемы с помощью TryCatch](../../../docs/framework/windows-workflow-foundation/samples/fault-handling-in-a-flowchart-activity-using-trycatch.md)  
  
    -   [Сценарий конечного автомата с использованием сочетания действий FlowChart и Pick](../../../docs/framework/windows-workflow-foundation/samples/statemachine-scenario-using-a-combination-of-flowchart-and-pick.md)  
  
    -   [Процесс найма](../../../docs/framework/windows-workflow-foundation/samples/hiring-process.md)  
  
-   Документация по конструктору:  
  
    -   [Конструктор действия блок\-схемы](../Topic/Flowchart%20Activity%20Designers.md)  
  
### Сценарии блок\-схем  
 Действие блок\-схемы можно использовать для реализации игры по угадыванию числа.Эта игра очень проста: компьютер выбирает случайное число, а игрок должен его угадать.Когда игрок дает ответ, компьютер выводит указание \(например,«попробуйте меньшее число»\).Если игрок угадывает число менее чем за 7 попыток, то он получает особое поздравление от компьютера.Эта игра может быть реализована с помощью сочетания следующих процедурных действий:  
  
-   <xref:System.Activities.Statements.Sequence>  
  
-   <xref:System.Activities.Statements.While>  
  
-   <xref:System.Activities.Statements.Switch%601>  
  
-   <xref:System.Activities.Statements.TryCatch>  
  
-   <xref:System.Activities.Statements.Assign%601>  
  
-   <xref:System.Activities.Statements.If>  
  
## Процедурные действия \(Sequence, If, ForEach, Switch, Assign, DoWhile, While\)  
 Процедурные действия предоставляют механизм моделирования последовательного потока управления, используя знакомые программистам концепции.Эти действия используют традиционно структурированные конструкции языка программирования и при необходимости предоставляют соответствие с распространенными процедурными языками, такими как C\# и VB.  
  
### Приступая к работе  
  
-   В [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)] создайте консольное приложение рабочего процесса.Добавьте в конструкторе рабочих процессов процедурные действия.  
  
-   Образцы:  
  
    -   [Процесс найма](../../../docs/framework/windows-workflow-foundation/samples/hiring-process.md)  
  
    -   [Процесс корпоративных закупок](../../../docs/framework/windows-workflow-foundation/samples/corporate-purchase-process.md)  
  
-   Документация по конструктору:  
  
    -   [Конструктор действия Parallel](../Topic/Parallel%20Activity%20Designer.md)  
  
    -   [Конструктор действия ParallelForEach\<T\>](../Topic/ParallelForEach%3CT%3E%20Activity%20Designer.md)  
  
### Сценарии процедурных действий  
  
-   <xref:System.Activities.Statements.Parallel>Parallel: система управления документами в интрасети имеет рабочий процесс утверждения документа.Документы перед публикацией в интрасети должны утверждаться сотрудниками нескольких отделов.Установленного порядка утверждений нет; они могут выполняться в любое время, пока документ находится в состоянии ожидания утверждения.Когда пользователь получает документ для рецензирования, он должен быть утвержден непосредственным руководителем, администратором интрасети и менеджером по внутренним коммуникациям.  
  
-   <xref:System.Activities.Statements.ParallelForEach%601>: приложение WF управляет корпоративными закупками в большой компании.Корпоративные правила предписывают перед планированием каждой операции закупки произвести оценку трех разных поставщиков.Сотрудник отдела, выполняющего закупку, выбирает трех поставщиков из списка поставщиков компании.После того как эти поставщики выбраны и проинформированы, компания ожидает от них коммерческих предложений.Предложения могут поступить в любом порядке.Чтобы реализовать этот сценарий в WF, выполните действие <xref:System.Activities.Statements.ParallelForEach%601> для всех поставщиков в коллекции, запросив от них коммерческие предложения.После того как все предложения собраны, выбирается и отображается лучшее из них.  
  
## InvokeMethod  
 Действие <xref:System.Activities.Statements.InvokeMethod> позволяет вызывать открытые методы для объектов или типов в области.Оно поддерживает вызов методов экземпляров и статических методов с параметрами или без параметров \(включая массивы параметров\) и универсальных методов.Оно также позволяет выполнять метод синхронно и асинхронно.  
  
### Приступая к работе  
  
-   В [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)] создайте консольное приложение рабочего процесса.Добавьте действие <xref:System.Activities.Statements.InvokeMethod> в конструкторе рабочих процессов и настройте для него метод экземпляра и статический метод.  
  
-   Образцы:  
  
    -   [InvokeMethod](../../../docs/framework/windows-workflow-foundation/samples/invokemethod.md)  
  
-   Документация по конструктору: [Конструктор действия InvokeMethod](../Topic/InvokeMethod%20Activity%20Designer.md)  
  
### Сценарии InvokeMethod  
  
-   Необходимо вызвать метод для объекта в области.Например, в словарь необходимо добавить значение.Вызывается метод Add для экземпляра словаря, указываются ключ и значение.  
  
-   Метод необходимо вызывать для унаследованного объекта CLR.Вместо создания пользовательского действия для заключения вызова унаследованного класса в оболочку, если он находится в области во время выполнения рабочего процесса, можно использовать <xref:System.Activities.Statements.InvokeMethod>.  
  
## Действия по обработке ошибок  
 Действие <xref:System.Activities.Statements.TryCatch> предоставляет механизм для перехвата исключений, возникающих во время выполнения набора содержащихся действий \(аналогично конструкции Try\/Catch в C\# и VB\).<xref:System.Activities.Statements.TryCatch> обеспечивает обработку исключений на уровне рабочего процесса.При возникновении необработанного исключения рабочий процесс прерывается и блок Finally не будет выполнен.Такое поведение согласуется с C\#.  
  
### Начало работы  
  
-   В [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)] создайте консольное приложение рабочего процесса.В конструкторе рабочих процессов добавьте действие <xref:System.Activities.Statements.TryCatch>.  
  
-   Образцы:  
  
    1.  [Обработка ошибок в действии блок\-схемы с помощью TryCatch](../../../docs/framework/windows-workflow-foundation/samples/fault-handling-in-a-flowchart-activity-using-trycatch.md)  
  
    2.  [Использование процедурных действий](../../../docs/framework/windows-workflow-foundation/samples/using-procedural-activities.md)  
  
-   Документация по конструктору: [Конструкторы действий обработки ошибок](../Topic/Error%20Handling%20Activity%20Designers.md)  
  
### Сценарии обработки ошибок  
 При возникновении ошибки должен быть выполнен набор действий и определенная логика.Если логика обработки ошибок обнаружила, что ошибку устранить нельзя, то исключение будет выдано повторно и проблема будет обрабатываться родительским действием \(или узлом\).  
  
## Действие Pick  
 Действие <xref:System.Activities.Statements.Pick> обеспечивает моделирование потока управления на основе событий в WF.Класс <xref:System.Activities.Statements.Pick> содержит множество ветвей, каждая из которых перед выполнением ожидает наступления конкретного события.В такой конфигурации действие <xref:System.Activities.Statements.Pick> ведет себя подобно <xref:System.Activities.Statements.Switch%601>, в котором действие выполнено только для одного события из набора прослушиваемых событий.Всеми ветвями управляют события, и появившееся событие запускает соответствующую ветвь.Все другие ветви отменяются и прекращают ожидать передачу данных, связанных с событиями.  
  
### Приступая к работе  
  
-   В [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)] создайте консольное приложение рабочего процесса.В конструкторе рабочих процессов добавьте действие <xref:System.Activities.Statements.Pick>.  
  
-   Образец: [Использование действия Pick](../../../docs/framework/windows-workflow-foundation/samples/using-the-pick-activity.md)  
  
-   Документация по конструктору: [Конструктор действия Pick](../Topic/Pick%20Activity%20Designer.md)  
  
### Сценарий Pick  
 Пользователь должен получать приглашение ввести данные.В обычных условиях разработчик может для запроса пользовательского ввода вызвать такой метод, как <xref:System.Console.ReadLine%2A>.Проблема в данном случае состоит в том, что программа должна ожидать ввода данных пользователем.В этом сценарии для разблокирования блокирующего действия необходимо время ожидания.В распространенном сценарии задача должна быть выполнена в течение заданного промежутка времени.Использование времени ожидания для блокирующего действия — это сценарий, где действие Pick имеет очень большое значение.  
  
## Служба маршрутизации WCF  
 Служба маршрутизации разработана как универсальный программный маршрутизатор для управления потоком сообщений [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] между клиентами и службами. Служба маршрутизации позволяет отсоединять клиенты от служб, что обеспечивает гораздо большую свободу выбора поддерживаемых конфигураций и гибкость при размещении служб. В .NET 3.5 клиенты и службы были тесно связаны, клиент должен был иметь сведения обо всех службах, с которыми он должен обмениваться данными, и об их расположении.Кроме того, служба WCF в .NET Framework 3.5 имела следующие ограничения.  
  
-   Обработка ошибок была сложной задачей, так как эта логика должна была быть жестко закодирована в клиенте.  
  
-   Клиенты и службы должны были всегда использовать одни и те же привязки.  
  
-   Службы редко были хорошо факторизованы: проще настроить клиент для работы с одной службой, реализующей все, что нужно, чем выбирать из множества служб.  
  
 Служба маршрутизации в .Net 4 позволяет упростить решение этих проблем.Новая служба маршрутизации имеет следующие функциональные возможности:  
  
1.  Маршрутизация на основе содержимого \(Объекты <xref:System.ServiceModel.Dispatcher.MessageFilter> исследуют сообщение и определяют, куда оно должно быть отправлено.\)  
  
2.  Связывание протоколов \(транспортного и сообщений\)  
  
3.  Обработка ошибок \(маршрутизатор перехватывает исключения и при возникновении сбоя переходит к резервным конечным точкам\)  
  
4.  Динамическое \(в памяти\) обновление <xref:System.ServiceModel.Dispatcher.MessageFilterTable%601> и конфигурации маршрутизации.  
  
### Приступая к работе  
  
1.  Документация: [Маршрутизация](../../../docs/framework/wcf/feature-details/routing.md)  
  
2.  Образцы: [Службы маршрутизации &#91;образцы WCF&#93;](../../../docs/framework/wcf/samples/routing-services.md)  
  
3.  Блог: [Правила маршрутизации\!](http://go.microsoft.com/fwlink/?LinkId=204956)  
  
### Сценарии маршрутизации  
 Служба маршрутизации полезна в следующих сценариях.  
  
-   Клиенты могут работать с несколькими службами, не обращаясь к ним непосредственно.  
  
-   Клиенты могут выполнять дополнительные операции с запросами, чтобы определить, куда их направить.  
  
-   Распределение операций, выполняемых клиентом, между несколькими реализациями службы без оптимизации кода клиента.  
  
-   Клиенты и службы могут согласовать различные привязки с различными параметрами безопасности.  
  
-   Клиенты могут быть более устойчивыми к сбоям или недоступности служб.  
  
## Обнаружение WCF  
 Обнаружение [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] — это технология платформы, позволяющая внедрять механизм обнаружения в инфраструктуру приложения.Его можно использовать для того, чтобы сделать службы доступными для обнаружения и настроить на клиентах поиск служб.Конечные точки больше не нужно жестко прописывать в клиентах, что позволяет делать приложения более надежными и отказоустойчивыми.Обнаружение — это превосходная основа для создания возможностей автоматической настройки приложений.  
  
 Продукт создается по стандарту WS\-Discovery.Он обладает возможностью взаимодействия, расширяемости и универсальности.Продукт поддерживает два режима функционирования.  
  
1.  Управляемый: в сети имеется сущность, осведомленная о существующих службах; клиенты направляют запросы непосредственно к ней.Такая схема работы аналогична Active Directory.  
  
2.  Нерегламентированный: клиенты используют многоадресные сообщения для обнаружения служб.  
  
 Более того, сообщения обнаружения не зависят от сетевого протокола; их можно использовать с любым протоколом, поддерживающим требования режима.Например, многоадресные сообщения обнаружения можно отправлять по каналу UDP или по любой другой сети, поддерживающей многоадресные сообщения. Эти расчетные точки в сочетании с гибкостью функций позволяют приспосабливать механизм обнаружения к различным решениям.  
  
### Приступая к работе  
  
-   Документация: [Обнаружение WCF](../../../docs/framework/wcf/feature-details/wcf-discovery.md)  
  
-   Образцы: [Обнаружение \(образцы\)](../../../docs/framework/wcf/samples/discovery-samples.md)  
  
### Сценарии обнаружения  
 Разработчик не хочет жестко задавать конечные точки, хотя неизвестно, когда служба будет доступна.Вместо этого разработчик хочет выбирать службу во время выполнения.Компоненты в приложении должны быть лучше разделены, более надежны и доступны для автоматической настройки.  
  
## Отслеживание  
 Отслеживание рабочих процессов обеспечивает понимание выполнения экземпляра рабочего процесса. События отслеживания создаются на уровне экземпляра рабочего процесса при выполнении действий в рабочем процессе.Участник отслеживания в рабочем процессе должен быть добавлен к узлу рабочего процесса для подписки на записи отслеживания.Записи отслеживания фильтруются с помощью профиля отслеживания.Платформа .Net Framework предоставляет участника отслеживания трассировки событий Windows \(средство отслеживания событий для Windows\). Базовый профиль задается в файле machine.config.  
  
### Приступая к работе  
  
1.  В [!INCLUDE[vs2010](../../../includes/vs2010-md.md)] создайте проект служебного приложения рабочего процесса WCF.Пара <xref:System.ServiceModel.Activities.Receive> и <xref:System.ServiceModel.Activities.SendReply> будет расположена на полотне для запуска.  
  
2.  Откройте файл web.config и добавьте поведение отслеживания трассировки событий Windows без профиля.  
  
    1.  Будет использован профиль по умолчанию.  
  
    2.  Откройте средство просмотра событий и включите канал аналитики для следующего узла: **Просмотр событий**, **Журналы приложений и служб**, **Microsoft**, **Windows**, **Сервер приложений\-Приложения**.Щелкните правой кнопкой мыши пункт **Аналитический** и выберите команду **Включить журнал**.  
  
    3.  Запустите службу рабочего процесса.  
  
    4.  Просмотрите события отслеживания рабочего процесса в средстве просмотра событий.  
  
3.  Образцы: [Отслеживание](../../../docs/framework/windows-workflow-foundation/samples/tracking.md)  
  
4.  Основная документация: [Отслеживание и трассировка рабочих процессов](../../../docs/framework/windows-workflow-foundation//workflow-tracking-and-tracing.md)  
  
## Хранилище экземпляров рабочих процессов SQL  
 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> — это реализация хранилища экземпляров на основе SQL Server.Хранилище экземпляров служит для хранения состояния запущенного экземпляра вместе со всеми данными, необходимыми для загрузки и возобновления работы экземпляра.Узел службы сохраняет состояние экземпляра в хранилище экземпляров при сохранении рабочего процесса, а также загружает состояние экземпляра при получении сообщения для этого экземпляра или после истечения срока действия действий задержки.  
  
### Приступая к работе  
  
1.  В [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)] создайте рабочий процесс, содержащий неявное или явное действие <xref:System.Activities.Statements.Persist>.Добавьте поведение <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> на узел службы рабочего процесса.Это можно сделать в коде или в файле конфигурации приложения.  
  
2.  Образцы: [Сохраняемость](../../../docs/framework/windows-workflow-foundation/samples/persistence.md)  
  
3.  Основная документация: [Хранилище экземпляров рабочих процессов SQL](../../../docs/framework/windows-workflow-foundation//sql-workflow-instance-store.md).