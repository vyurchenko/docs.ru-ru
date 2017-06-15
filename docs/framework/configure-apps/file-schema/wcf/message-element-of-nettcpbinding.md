---
title: "Элемент &lt;message&gt; &lt;netTcpBinding&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1d71edd9-c085-4c2e-b6d3-980c313366f9
caps.latest.revision: 20
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 20
---
# Элемент &lt;message&gt; &lt;netTcpBinding&gt;
Определяет тип требований безопасности уровня сообщений для конечных точек, настроенных с элементом [\<netTcpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/nettcpbinding.md).  
  
## Синтаксис  
  
```  
  
<message   
      algorithmSuite=System.Servicemodel.Security.SecurityAlgorithmsuite  
    clientCredentialType="None/Windows/UserName/Certificate/IssuedToken"/>  
```  
  
## Атрибуты и элементы  
 В следующих разделах описаны атрибуты, дочерние и родительские элементы.  
  
### Атрибуты  
  
|Атрибут|Описание|  
|-------------|--------------|  
|`algorithmSuite`|Задает алгоритмы шифрования сообщений и ключей.  Алгоритмы и размеры ключей определяются классом <xref:System.ServiceModel.Security.SecurityAlgorithmSuite>.  Эти алгоритмы соответствуют алгоритмам, заданным в спецификации языка политики безопасности \(WS\-SecurityPolicy\).<br /><br /> В следующей таблице представлены возможные значения.  Значение по умолчанию — `Basic256`.<br /><br /> Если привязка службы определяет значение `algorithmSuite`, которое отличается от значения по умолчанию, а файл конфигурации создается с помощью программы Svcutil.exe, значит файл создается неправильно и необходимо вручную исправить файл конфигурации, чтобы присвоить атрибуту нужное значение.|  
|`clientCredentialType`|Задает тип учетных данных, используемых при проверке подлинности клиента с помощью правил безопасности уровня сообщений.  В следующей таблице представлены возможные значения.  Значение по умолчанию — `UserName`.  Это атрибут типа <xref:System.ServiceModel.MessageCredentialType>.|  
  
## Атрибут algorithmSuite  
  
|Значение|Описание|  
|--------------|--------------|  
|Basic128|Используется шифрование Aes128, Sha1 для хэша и Rsa\-oaep\-mgf1p для шифрования ключа.|  
|Basic192|Используется шифрование Aes192, Sha1 для хэша и Rsa\-oaep\-mgf1p для шифрования ключа.|  
|Basic256|Используется шифрование Aes256, Sha1 для хэша и Rsa\-oaep\-mgf1p для шифрования ключа.|  
|Basic256Rsa15|Используется Aes256 для шифрования сообщения, Sha1 для хэша и Rsa15 для шифрования ключа.|  
|Basic192Rsa15|Используется Aes192 для шифрования сообщения, Sha1 для хэша и Rsa15 для шифрования ключа.|  
|TripleDes|Используется шифрование TripleDes, Sha1 для хэша и Rsa\-oaep\-mgf1p для шифрования ключа.|  
|Basic128Rsa15|Используется Aes128 для шифрования сообщения, Sha1 для хэша и Rsa15 для шифрования ключа.|  
|TripleDesRsa15|Используется TripleDes для шифрования сообщения, Sha1 для хэша и Rsa15 для шифрования ключа.|  
|Basic128Sha256|Используется Aes256 для шифрования сообщения, Sha256 для хэша и Rsa\-oaep\-mgf1p для шифрования ключа.|  
|Basic192Sha256|Используется Aes192 для шифрования сообщения, Sha256 для хэша и Rsa\-oaep\-mgf1p для шифрования ключа.|  
|Basic256Sha256|Используется Aes256 для шифрования сообщения, Sha256 для хэша и Rsa\-oaep\-mgf1p для шифрования ключа.|  
|TripleDesSha256|Используется TripleDes для шифрования сообщения, Sha256 для хэша и Rsa\-oaep\-mgf1p для шифрования ключа.|  
|Basic128Sha256Rsa15|Используется Aes128 для шифрования сообщения, Sha256 для хэша и Rsa15 для шифрования ключа.|  
|Basic192Sha256Rsa15|Используется Aes192 для шифрования сообщения, Sha256 для хэша и Rsa15 для шифрования ключа.|  
|Basic256Sha256Rsa15|Используется Aes256 для шифрования сообщения, Sha256 для хэша и Rsa15 для шифрования ключа.|  
|TripleDesSha256Rsa15|Используется TripleDes для шифрования сообщения, Sha256 для хэша и Rsa15 для шифрования ключа.|  
  
## Атрибут clientCredentialType  
  
|Значение|Описание|  
|--------------|--------------|  
|Нет|Данный атрибут позволяет службе взаимодействовать с анонимными клиентами.  Для службы это означает, что она не требует учетных данных клиента.  Для клиента это означает, что он не должен предоставлять никаких учетных данных.|  
|Windows|Атрибут позволяет проводить обмен сообщениями SOAP, если выполнена проверка подлинности с помощью учетных данных Windows.|  
|UserName|Позволяет службе запрашивать проверку подлинности клиента на основе учетных данных типа UserName.  [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] не поддерживает передачу дайджеста пароля или получение ключей с использованием пароля и использование таких ключей для обеспечения безопасности сообщений.  Таким образом, служба [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] принудительно обеспечивает безопасность транспорта при использовании учетных данных UserName.  Результатом использования такого режима работы с учетными данными является либо обмен с возможностью взаимодействия, либо согласование без возможности взаимодействия в зависимости от атрибута `negotiateServiceCredential`.|  
|Сертификат|Позволяет службе требовать проверки подлинности клиента с помощью сертификата.  Если используется режим безопасности message и атрибут `negotiateServiceCredential` имеет значение `false`, то клиенту должен быть предоставлен сертификат службы.|  
|IssuedToken|Задает пользовательский маркер, который обычно выдается службой маркеров безопасности \(STS\).|  
  
### Дочерние элементы  
 Нет  
  
### Родительские элементы  
  
|Элемент|Описание|  
|-------------|--------------|  
|[\<безопасность\>](../../../../../docs/framework/configure-apps/file-schema/wcf/security-of-nettcpbinding.md)|Определяет возможности безопасности для элемента <xref:System.ServiceModel.Configuration.NetTcpBindingElement>.|  
  
## Заметки  
 При передаче сообщений используется безопасность уровня сообщений для обеспечения конфиденциальности и целостности сообщений SOAP, а также для взаимной проверки подлинности одноранговых узлов.  Если данный режим безопасности выбран для привязки, стек каналов настраивается с элементами привязки безопасности сообщений и сообщения SOAP защищаются в соответствии со стандартами WS\-Security\*.  
  
## См. также  
 <xref:System.ServiceModel.MessageSecurityOverTcp>   
 <xref:System.ServiceModel.Configuration.NetTcpSecurityElement.Message%2A>   
 <xref:System.ServiceModel.NetTcpSecurity.Message%2A>   
 <xref:System.ServiceModel.Configuration.NetTcpSecurityElement>   
 [Защита служб и клиентов](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [Привязки](../../../../../docs/framework/wcf/bindings.md)   
 [Настройка привязок, предоставляемых системой](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)   
 [Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/ru-ru/bd8b277b-932f-472f-a42a-b02bb5257dfb)   
 [\<привязка\>](../../../../../docs/framework/misc/binding.md)