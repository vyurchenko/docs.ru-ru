---
title: "Управление приостановленным экземпляром | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f5ca3faa-ba1f-4857-b92c-d927e4b29598
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Управление приостановленным экземпляром
Этот образец демонстрирует управление экземплярами рабочего процесса, которые были приостановлены.Действием по умолчанию для поведения <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionBehavior> является `AbandonAndSuspend`.Это означает, что по умолчанию при появлении необработанных исключений, сформированных экземпляром рабочего процесса, который размещен на узле <xref:System.ServiceModel.WorkflowServiceHost>, экземпляр удаляется из памяти \(отбрасывается\) и устойчивая\/сохраненная версия экземпляра отмечается как приостановленная.Приостановленный экземпляр рабочего процесса не будет в состоянии выполняться до отмены приостановки.  
  
 Этот образец показывает, как можно реализовать программу командной строки для выполнения запроса приостановленных экземпляров и как дать пользователю возможность возобновлять или завершать работу экземпляра.В этом образце служба рабочего процесса преднамеренно вызывает исключение, в результате чего она приостанавливается.Затем с помощью программы командной строки можно будет запросить экземпляр, а после этого возобновить или завершить его работу.  
  
## Демонстрации  
 Узел <xref:System.ServiceModel.WorkflowServiceHost> с поведением <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionBehavior> и <xref:System.ServiceModel.Activities.WorkflowControlEndpoint> в [!INCLUDE[wf](../../../../includes/wf-md.md)].  
  
## Обсуждение  
 Программа командной строки, реализованная в этом образце, предназначена для работы с реализацией хранилища экземпляра SQL Server, который поставляется в [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)].Если имеется пользовательская реализация хранилища экземпляра, то можно приспособить и эту программу, заменяя в образце реализации `WorkflowInstanceCommand` реализациями, которые относятся к применяемому хранилищу экземпляра.  
  
 Команды SQL в предоставленной реализации запускаются непосредственно по отношению к хранилищу экземпляра SQL для формирования списка приостановленных экземпляров, а для возобновления или завершения работы экземпляров в ней используется конечная точка <xref:System.ServiceModel.Activities.WorkflowControlEndpoint>, добавленная к узлу <xref:System.ServiceModel.WorkflowServiceHost>.  
  
#### Настройка, построение и выполнение образца  
  
1.  Для этого образца необходимо включить следующие компоненты Windows.  
  
    1.  Сервер очереди сообщений \(Майкрософт\) \(MSMQ\)  
  
    2.  SQL Server Express  
  
2.  Установка базы данных SQL Server.  
  
    1.  В командной строке [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] выполните команду «setup.cmd» в каталоге образцов SuspendedInstanceManagement, которая выполняет следующее.  
  
        1.  Создает базу данных сохраняемости с использованием SQL Server Express.Если база данных сохраняемости уже существует, то она будет удалена и создана повторно.  
  
        2.  Настраивает базу данных с учетом требований сохраняемости.  
  
        3.  Добавляет IIS APPPOOL\\DefaultAppPool and NT AUTHORITY\\Network Service к роли InstanceStoreUsers, которая была определена при настройке базы данных для сохраняемости.  
  
3.  Настройка очереди обслуживания.  
  
    1.  В [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] щелкните правой кнопкой мыши проект **SampleWorkflowApp** и выберите команду **Назначить запускаемым проектом**.  
  
    2.  Скомпилируйте и запустите образец SampleWorkflowApp, нажав клавишу **F5**.Будет создана требуемая очередь.  
  
    3.  Нажмите клавишу **ВВОД**, чтобы остановить приложение SampleWorkflowApp.  
  
    4.  Откройте консоль «Управление компьютером», выполнив команду Compmgmt.msc из командной строки.  
  
    5.  Разверните узлы **Служба и приложения**, **Очередь сообщений**, **Частные очереди**.  
  
    6.  Щелкните очередь **ReceiveTx** правой кнопкой мыши и выберите команду **Свойства**.  
  
    7.  Перейдите на вкладку **Безопасность** и предоставьте роли **Все** разрешения **Получение сообщения**, **Просмотр сообщения** и **Отправка сообщения**.  
  
4.  После этого выполните образец.  
  
    1.  В [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] снова запустите проект SampleWorkflowApp без отладки, нажав клавиши **Ctrl\+F5**.В окне консоли будут выведены два адреса конечных точек: один для конечной точки приложения и еще один из <xref:System.ServiceModel.Activities.WorkflowControlEndpoint>.Затем будет создан экземпляр рабочего процесса и в окне консоли появятся записи отслеживания для этого экземпляра.Экземпляр рабочего процесса вызовет исключение, в результате чего работа экземпляра будет приостановлена и прервана.  
  
    2.  После этого с помощью программы командной строки можно будет выполнить дальнейшие действий с любым из этих экземпляров.Синтаксис аргументов командной строки:  
  
         `SuspendedInstanceManagement -Command:[ИмяКоманды] -Server:[ИмяСервера] -Database:[ИмяБазыДанных] -InstanceId:[ИдентификаторЭкземпляра]`  
  
         Поддерживаемые команды: `Query`, `Resume` и `Terminate`.Параметр InstanceId требуется только для операций `Resume` и `Terminate`.  
  
#### Очистка \(необязательно\)  
  
1.  Откройте консоль управления компьютером, запустив команду Compmgmt.msc в командной строке `vs2010`.  
  
2.  Разверните узлы **Служба и приложения**, **Очередь сообщений**, **Частные очереди**.  
  
3.  Удалите очередь **ReceiveTx**.  
  
4.  Для удаления базы данных сохраняемости выполните команду cleanup.cmd.  
  
> [!IMPORTANT]
>  Образцы уже могут быть установлены на компьютере.Перед продолжением проверьте следующий каталог \(по умолчанию\).  
>   
>  `<диск_установки>:\WF_WCF_Samples`  
>   
>  Если этот каталог не существует, перейдите на страницу [Образцы Windows Communication Foundation \(WCF\) и Windows Workflow Foundation \(WF\) для .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780), чтобы загрузить все образцы [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] и [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Этот образец расположен в следующем каталоге.  
>   
>  `<диск_установки>:\WF_WCF_Samples\WF\Application\SuspendedInstanceManagement`