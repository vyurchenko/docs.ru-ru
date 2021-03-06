---
title: "Образец элемента привязки для обнаружения | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: af513015-85bf-417b-8729-1bdff77ff6d6
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# Образец элемента привязки для обнаружения
Данный образец демонстрирует использование клиентского элемента привязки обнаружения для обнаружения службы.Эта функция позволяет разработчикам добавлять клиентский канал обнаружения к клиентскому стеку каналов, в результате чего модель программирования становится намного интуитивно понятнее.Если соответствующий канал открыт, адрес службы разрешается в процессе обнаружения.Данный образец состоит из следующих проектов.  
  
-   **CalculatorService**: доступная для обнаружения служба [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
-   **CalculatorClient**: клиентское приложение [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], которое использует клиентский канал обнаружения для поиска и вызова службы CalculatorService.  
  
-   **DynamicCalculatorClient**: клиентское приложение [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], которое использует динамическую конечную точку для поиска и вызова службы CalculatorService.  
  
> [!IMPORTANT]
>  Образцы уже могут быть установлены на компьютере.Перед продолжением проверьте следующий каталог \(по умолчанию\).  
>   
>  `<диск_установки>:\WF_WCF_Samples`  
>   
>  Если этот каталог не существует, перейдите на страницу [Образцы Windows Communication Foundation \(WCF\) и Windows Workflow Foundation \(WF\) для .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780), чтобы загрузить все образцы [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] и [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Этот образец расположен в следующем каталоге.  
>   
>  `<диск_установки>:\WF_WCF_Samples\WCF\Basic\Discovery\DiscoveryBindingElement`  
  
## CalculatorService  
 Данный проект содержит простую службу калькулятора, которая реализует контракт `ICalculatorService`.  
  
 Следующий файл App.config используется для добавления поведения `<serviceDiscovery>` в набор поведений службы, а также конечной точки обнаружения.  
  
```  
<system.serviceModel>  
    <services>  
      <service behaviorConfiguration="CalculatorBehavior" name="Microsoft.Samples.Discovery.CalculatorService">  
        <endpoint name="udpDiscoveryEpt" kind="udpDiscoveryEndpoint" />  
      </service>  
    </services>  
    <behaviors>  
      <!--Enable discovery through configuration.-->  
      <serviceBehaviors>  
        <behavior name="CalculatorBehavior">  
          <serviceDiscovery>  
          </serviceDiscovery>  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  </system.serviceModel>  
```  
  
 При этом служба и ее конечные точки становятся доступными для обнаружения.Служба CalculatorService представляет собой саморазмещаемую службу, которая добавляет одну конечную точку с использованием привязки NetTcpBinding.Кроме того, она добавляет в конечную точку поведение `EndpointDiscoveryBehavior` и указывает область, как показано в следующем примере кода.  
  
```  
// Add a NET.TCP endpoint and add a scope to that endpoint.  
ServiceEndpoint netTcpEndpoint = serviceHost.AddServiceEndpoint(typeof(ICalculatorService), new NetTcpBinding(), netTcpAddress);  
EndpointDiscoveryBehavior netTctEndpointBehavior = new EndpointDiscoveryBehavior();  
netTctEndpointBehavior.Scopes.Add(new Uri("ldap:///ou=engineering,o=exampleorg,c=us"));  
netTcpEndpoint.Behaviors.Add(netTctEndpointBehavior);  
serviceHost.Open();  
```  
  
## CalculatorClient  
 Данный проект содержит реализацию клиента, которая отправляет сообщения службе CalculatorService.Эта программа использует метод `CreateCustomBindingWithDiscoveryElement()` для создания пользовательской привязки, которая использует клиентский канал обнаружения.  
  
```  
static CustomBinding CreateCustomBindingWithDiscoveryElement()  
 {  
      DiscoveryClientBindingElement discoveryBindingElement = new DiscoveryClientBindingElement();  
  
            // Provide the search criteria and the endpoint over which the probe is sent  
            discoveryBindingElement.FindCriteria = new FindCriteria(typeof(ICalculatorService));  
            discoveryBindingElement.DiscoveryEndpointProvider = new UdpDiscoveryEndpointProvider();  
  
            CustomBinding customBinding = new CustomBinding(new NetTcpBinding());  
            // Insert DiscoveryClientBindingElement at the top of the BindingElement stack.  
            // An exception is thrown if this binding element is not at the top  
            customBinding.Elements.Insert(0, discoveryBindingElement);  
  
            return customBinding; }  
```  
  
 После создания экземпляра <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement> разработчик указывает критерии, используемые при поиске службы.В данном случае критерием обнаружения является тип `ICalculatorService`.Кроме того, разработчик указывает поставщика <xref:System.ServiceModel.Discovery.DiscoveryEndpointProvider>, который возвращает конечную точку <xref:System.ServiceModel.Discovery.DiscoveryEndpoint>, указывающую место поиска служб.Поставщик <xref:System.ServiceModel.Discovery.DiscoveryEndpointProvider> возвращает новый экземпляр конечной точки <xref:System.ServiceModel.Discovery.DiscoveryEndpoint>.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Использование пользовательской привязки для клиентского канала обнаружения](../../../../docs/framework/wcf/feature-details/using-a-custom-binding-with-the-discovery-client-channel.md).  
  
```  
// Extend DiscoveryEndpointProvider class to change the default DiscoveryEndpoint  
    // to the DiscoveryClientBindingElement. The Discovery ClientChannel   
    // uses this endpoint to send Probe message.  
    public class UdpDiscoveryEndpointProvider : DiscoveryEndpointProvider  
    {  
        public override DiscoveryEndpoint GetDiscoveryEndpoint()  
        {  
            return new UdpDiscoveryEndpoint(DiscoveryVersion.WSDiscoveryApril2005);  
        }  
    }  
```  
  
 В данном случае клиент использует многоадресный механизм UDP, определенный в протоколе обнаружения, для поиска служб в локальной подсети.В оставшейся части метода создается пользовательская привязка, и элемент привязки обнаружения вставляется в верхушку стека.  
  
> [!NOTE]
>  Элемент <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement> должен быть помещен в верхушку стека привязок.Любой элемент <xref:System.ServiceModel.Channels.BindingElement>, расположенный выше элемента <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement>, должен удостовериться, что создаваемые им фабрики каналов и каналы не используют свойства `EndpointAddress` и `Via`, поскольку фактический адрес становится известным только на уровне клиентского канала обнаружения.  
  
 После этого можно создать экземпляр `CalculatorClient`, передав ему эту пользовательскую привязку и адрес конечной точки.  
  
```  
CalculatorServiceClient client = new CalculatorServiceClient(CreateCustomBindingWithDiscoveryElement(), DiscoveryClientBindingElement.DiscoveryEndpointAddress);  
```  
  
 При использовании клиентского канала обнаружения передается постоянный адрес конечной точки, заданный ранее.Во время выполнения клиентский канал обнаружения находит службу, указываемую критерием поиска, и подключается к ней.Для установления соединения между службой и клиентом они также должны иметь один и тот же базовый стек привязок.  
  
#### Использование этого образца  
  
1.  Откройте решение в среде [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)].  
  
2.  Постройте решение.  
  
3.  Запустите приложение службы и каждое из клиентских приложений.  
  
4.  Заметьте, что клиенту удалось найти службу, не зная ее адреса.  
  
## См. также